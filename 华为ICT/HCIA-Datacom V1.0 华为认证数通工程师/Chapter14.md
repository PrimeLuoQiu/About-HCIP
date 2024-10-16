# 网络地址转换

## NAT概念

提出原因：IPv4的地址不够用

### 私网IP地址

- 公有地址：由专门的机构管理、分配，可以在Internet上直接通信的IP地址
- 私有地址：组织和个人可以随意使用，无法在Internet上直接通信，只能在内网使用的IP地址
- A、B、C类地址中各预留了一些地址作为专门作为私有IP地址
  - A类：10.0.0.0~10.255.255.255
  - B类：172.16.0.0~172.31.255.255
  - C类：192.168.0.0~192.168.255.255

公有地址需要申请且具有唯一性，两个私网地址之间不可以进行通信，当需要访问外网的时候，这个时候需要换一个马甲，将自己的私有地址转换成公有地址，这就是NAT技术

### NAT技术原理

- NAT：对IP数据报文的IP地址进行转换，部署在网络出口设备，例如路由器或者防火墙。
- NAT的典型应用场景
  - 对于从内到外的流量，网络设备通过NAT将数据包的源地址进行转换
  - 对于外到内的流量，则对数据包的目的地址进行转换。

访问公网的时候地址不能冲突

原IP替换

公司内网架web 外网也要访问 不能使用私有 对外呈现公有地址的一个角色，然后外网访问内网的时候，先访问外网的IP，然后转换到内网的IP

![image-20241016201024177](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016201024177.png)

## 静态NAT

这种静态转换的过程是需要网络管理员去进行一一对应的配置的。类似于静态路由的表，一个私网IP对应的是一个公网IP，需要手动的一一对应，如果要进行更改的话，也需要管理员去手动的进行更改和添加。

转换的时候目的ip是不变的，原IP是变化的。

![image-20241016201654158](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016201654158.png)

外网ping内网也是一样的不可通

### 静态NAT配置介绍

1.方式一：接口视图下配置静态NAT

---

[Huawei-GigabitEthernet0/0/0] **nat static global** {*global-address*}**inside**{*host-address*

---

global参数用于配置外部公有地址，inside参数用于配置内部私有地址

方式二是和方式一一样，在系统视图下配置，但是配置完之后需要在对应的接口下进行使能就是`nat static enable`

## 动态NAT

静态NAT实际上还是没有解决公网IP不够用的问题，这个时候如果能把公网IP地址作为一个地址池，然后谁需要谁取就好了，那么就引入了动态NAT

### 动态NAT原理

当内部主机访问外部网络时临时分配一个地址池中未使用的地址，并将该地址标记为"In Use"。当该主机不再访问外部网路时回收分配的地址，重新标记为"Not Use"

![image-20241016204406966](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016204406966.png)![image-20241016204550630](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016204550630.png)

![image-20241016204639878](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016204639878.png)

### 动态NAT配置介绍

1.创建地址池

---

[Huawei]**nat address-group** *group-index start-address end-address*

---

配置公有地址范围，其中group-index为地址池编号，start-address、end-address分别为地址池起始地址、结束地址

2.配置地址转换的ACL规则

---

[Huawei]**acl** number

[Huawei-acl-basic-*number*]**rule permit source** *source-address source-wildcad*

---

配置基础ACL，匹配需要进行动态转换的源地址范围

3.接口视图下配置带地址池的NAT Outbound

---

[Huawei-GigabitEthernet0/0/0]**nat outbound** *acl-number* **address-group** *group-index*[**no-pat**]

---

接口下关联ACL与地址池进行动态地址转换，no-pat参数指定不进行端口转换

no-pat指的是只换IP地址信息，不换端口号信息

![image-20241016205413475](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016205413475.png)

## NAPT、Easy-IP

### NAPT原理(Network Address and Port Translation)

网络接口地址转换：从地址池中选择地址进行地址转换时不仅转换IP地址，同时也会对端口号进行转换，从而实现公有地址和私有地址的1:n映射，可以有效的提高公有地址利用率



其实就是，动态NAT只能保证每个人都有公网地址用，但是不能保证100个人同时进行使用，这个时候我们可以引用端口号的概念，一个IP下面对应的65536个端口号，那么也就意味着我们可以通过IP+对应端口号的方式来让多个人使用相同的IP。



![image-20241016210542531](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016210542531.png)



![image-20241016210642278](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016210642278.png)

映射表在这里是十分的重要的。

### 配置

![image-20241016210849364](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016210849364.png)

### Easy IP

实现原理和NAPT相同，同时转换IP地址、传输层接口、区别在于Easy IP没有地址池的概念，使用接口地址作为NAT转换的公有地址。

EasyIP适用于不具备固定公网IP地址的场景：如通过DHCP、PPPoE拨号获取地址的私有网络接口，可以直接使用获取到的动态地址进行转换



不需要配置地址池，出口的IP地址不固定，例如使用DHCP获取的地址，地址不一定是固定的。需要提供公有地址，但公有地址直接使用的是接口的IP地址，如果拿到的是1.1，大家就统一用1.1加端口号出去。

![image-20241016211256094](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016211256094.png)

![image-20241016211640428](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016211640428.png)

更加充分的利用公网地址

## NAT Server

### 使用场景

指定[公有地址:接口]与[私有地址:接口]的一一对应关系，将内网服务器映射到公网，当私有网络中的服务器需要对公网提供服务的时候使用。



其实就是只转换IP地址，不转换端口号，其他的端口号还可以给其他的主机进行公网的转换。

![image-20241016212520746](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016212520746.png)

### 转换示例

![image-20241016212541422](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016212541422.png)

进去的时候实际上修改的是目的地址，

### 配置示例

![image-20241016212655530](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016212655530.png)
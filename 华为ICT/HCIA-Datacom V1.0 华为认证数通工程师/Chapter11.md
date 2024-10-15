# OSPF基础

## OSPF协议概述

### 动态路由协议分类

- 静态路由有以下问题
  - 无法适应规模大的网络  一个一个静态配置管理员太累
  - 无法动态响应网络变化 但凡出现链路故障，如果管理员没有进行配置，那么就得重新进行配置。非常麻烦

按工作区域分类：

​	IGP 内部网关协议

​		RIP -> 路由信息协议

​		OSPF -> 最短路径优先协议

​		IS-IS -> 中间系统到中间系统

​	EGP 外部网关协议

​		BGP -> 边界网关协议

按工作机制及算法分类

​	距离路由适量协议Distance Vector Routing Protocols  取决于朋友路由器告诉怎么走，不知道整个的拓扑

​		RIP

​	链路状态路由协议Link-State Routing Protocols  有一个内部的数据库

​		OSPF

​		IS-IS

#### 距离矢量路由协议

因为所有的路由器的信息来源完全取决于别人告诉我应该怎么走

那么

- 运行距离矢量路由协议的路由器就会周期性的泛洪自己的路由表(将自己链路状态告诉其他所有路由器)
- 选择的依据在于别人告诉我应该怎么走，所以不一定是最优的
- 通告的是路由信息(算完的路径信息)

#### 链路状态路由协议-LSA泛洪

距离路由矢量协议由于所有来源都是它的邻居，那么选出来的路径可能就不是最优路径，而且还可能会存在环路



不再通告路由信息，而是LSA

LSA描述了路由器接口的状态信息，例如接口的开销，连接的对象



所有路由器都会将对应的LSA信息进行泛洪，在每台路由器上形成一个数据库



#### 链路状态路由协议-LSDB组建

- 路由器将LSA存放在LSDB中
- LSDB汇总了网络中路由器对于自己接口的描述
- LSDB包含全网拓扑的描述



#### 链路状态路由协议-SPF计算

每台路由器都计算出一颗以自己为根的、无环的、拥有最短路径的树。

有任何问题都会实时的告诉邻居，让邻居对响应状态进行更新。

算完之后是为了更新路由表

#### 链路状态路由协议-路由表生成

每台路由器根据SPF计算结果，将结果放入路由表



#### 总结

![image-20241015092246520](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015092246520.png)

### OSPF简介

#### OSPF简介

![image-20241015092707077](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015092707077.png)

路由汇总精简路由表

#### OSPF在园区网络中的应用。

主要应用于汇聚交换机和核心交换机之间的

![image-20241015092846502](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015092846502.png)

#### OSPF基础术语：区域

OSPF Area用于标识一个OSPF的区域。

区域是从逻辑上将设备划分为不同的组，每个组用区域号(Area ID)来标识。

好处就是，如果这个区域当中产生了动荡，那么只会影响到这个区域当中



#### OSPF基础术语：Router-ID

- 用于在一个OSPF域中唯一地标识一台路由器。
- 设定可以通过手工的方式，或系统自动配置



#### OSPF基础术语：度量值(Cost)

使用Cost值作为路由的度量值。

![image-20241015093458951](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015093458951.png)

如果有一个1G速率的接口，但是如果使用OSPF计算出来是0.1，但是OSPF没有小数点，也就意味着1G的接口也是1，接下来要么我们手动的去修改100M的接口速率为10，或者配置OSPF指定的缺省参考值，都是可以的。

![image-20241015093652977](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015093652977.png)

计算的时候是一个累积的和。

#### OSPF报文类型

有五种协议的报文

![image-20241015093949840](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015093949840.png)

摘要信息类似目录，让对方路由器与自身信息进行一个对比，如果有不一样的，那么对方会发送一个LSRequest报文进行请求，然后我们再发送一个LSU报文向其发送其的请求，接下来对方如果收到之后且确认收到的话，会发送一个LSA报文对我发送的信息进行一个确认。

#### OSPF三大表项-邻居表

![image-20241015094546502](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015094546502.png)

![image-20241015094618829](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015094618829.png)

#### OSPF三大表项-LSDB表

![image-20241015095515806](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015095515806.png)

类型：本区域产生的/特殊路由器产生的

#### OSPF三大表项-OSPF路由表

![image-20241015095807978](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015095807978.png)

OSPF路由表和IP路由表是两个概念，IP中的不一定会有OSPF中的，OSPF在经过择优计算之后，会放入到最终的IP路由表当中

同一目的地不同来源会在比较后加入IP路由表 

## OSPF协议工作原理

### OSPF邻居建立

- OSPF路由器之间关系有两个重要概念，分别是邻居关系和邻接关系
  - 在两台路由器直连的情况下，在通过hello报文发现彼此之后，两台路由器实现了邻居关系
  - 当两台路由器LSDB同步完成，结束了一系列的报文交互之后并开始独立计算路由的时候，就形成了邻接关系

### 建立过程

![image-20241015103824260](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015103824260.png)

#### OSPF邻接关系建立流程

![image-20241015104203462](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015104203462.png)

• 当一台OSPF路由器收到其他路由器发来的首个Hello报文时会从初始Down状态切换为Init状态。 

• 当OSPF路由器收到的Hello报文中的邻居字段包含自己的Router ID时，从Init切换2-way状态。

![image-20241015104652387](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015104652387.png)

> • 邻居状态机从2-way转为Exstart状态后开始主从关系选举： 
>
> ​	▫ R1向R2发送的第一个DD报文内容为空，其Seq序列号假设为X。 
>
> ​	▫ R2也向R1发出第一个DD报文,其Seq序列号假设为Y。 
>
> ​	▫ 选举主从关系的规则是比较Router ID，越大越优。R2的Router ID比R1大，因此R2成为真正的主设备。主从关系比较结束后，R1的状态从Exstart转变为Exchange。 
>
> • R1邻居状态变为Exchange后，R1发送一个新的DD报文，包含自己LSDB的描述信息，其序 列号采用主设备R2的序列号。R2收到后邻居状态从Exstart转变为Exchange。 
>
> • R2向R1发送一个新的DD报文，包含自己LSDB的描述信息，序列号为Y+1。 
>
> • R1作为从路由器需要对主路由R2发送的每个DD报文进行确认，回复报文的序列号与主路由 R2一致。 
>
> • 发送完最后一个DD报文后，R1将邻居状态切换为Loading。

![image-20241015105524861](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015105524861.png)

> • 邻居状态转变为Loading后，R1向R2发送LSR报文，请求那些在Exchange状态下通过DD报文发现的，但是在本地LSDB中没有的LSA。 
>
> • R2收到后向R1回复LSU。在LSU报文中包含被请求的LSA的详细信息。 
>
> • R1收到LSU报文后，向R2回复LS ACK报文，确认已接收到，确保信息传输的可靠性。 
>
> • 此过程中R2也会向R1发送LSA请求。当两端LSDB完全一致时，邻居状态变为Full，表示成 功建立邻接关系。

#### OSPF邻居表回顾

![image-20241015105655055](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015105655055.png)

> • 如图所示输入display ospf peer命令之后，各项参数含义如下： 
>
> ​	▫ OSPF Process 1 with Router ID 1.1.1.1：本地OSPF进程号为1与本端OSPF Router ID 为1.1.1.1 
>
> ​	▫ Router ID：邻居OSPF路由器ID ▫ Address：邻居接口地址 
>
> ​	▫ GR State：使能OSPF GR功能后显示GR的状态（GR为优化功能），默认为Normal 
>
> ​	▫ State：邻居状态，正常情况下LSDB同步完成之后，稳定停留状态为Full 
>
> ​	▫ Mode：用于标识本台设备在链路状态信息交互过程中的角色是Master还是Slave 
>
> ​	▫ Priority：用于标识邻居路由器的优先级（该优先级用于后续DR角色选举） 
>
> ​	▫ DR：指定路由器 ▫ BDR：备份指定路由器 
>
> ​	▫ MTU：邻居接口的MTU值 
>
> ​	▫ Retrans timer interval：重传LSA的时间间隔，单位为秒 
>
> ​	▫ Authentication Sequence：认证序列号

### OSPF路由表建立

#### OSPF网络类型简介

![image-20241015110016733](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015110016733.png)

> • OSPF网络类型是一个非常重要的接口变量，这个变量将影响OSPF在接口上的操作，例如采用什么方式发送OSPF协议报文，以及是否需要选举DR、BDR等。 
>
> • 接口默认的OSPF网络类型取决于接口所使用的数据链路层封装。 
>
> • 如图所示，OSPF的有四种网络类型，Broadcast、NBMA、P2MP和P2P。

#### OSPF网络类型

![image-20241015110432617](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015110432617.png)

PPP 指的是 Point to Point Protocol 点对点协议

> • 一般情况下，链路两端的OSPF接口网络类型必须一致，否则双方无法建立邻居关系。 
>
> • OSPF网络类型可以在接口下通过命令手动修改以适应不同网络场景，例如可以将BMA网络 类型修改为P2P。

![image-20241015110529453](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015110529453.png)

#### DR与BDR的背景

![image-20241015111739916](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015111739916.png)

> • MA（Multi-Access）多路访问网络有两种类型：广播型多路访问网络（BMA）及非广播型多路访问网络（NBMA）。以太网（Ethernet）是一种典型的广播型多路访问网络。 
>
> • 在MA网络中，如果每台OSPF路由器都与其他的所有路由器建立OSPF邻接关系，便会导致网络中存在过多的OSPF邻接关系，增加设备负担，也增加了网络中泛洪的OSPF报文数量。 
>
> • 当拓扑出现变更，网络中的LSA泛洪可能会造成带宽的浪费和设备资源的损耗。

#### DR与BDR

![image-20241015111924079](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015111924079.png)

> • 选举规则：OSPF DR优先级更高的接口成为该MA的DR，如果优先级相等（默认为1），则 具有更高的OSPF Router-ID的路由器（的接口）被选举成DR，并且DR具有非抢占性。

#### OSPF域与单区域

![image-20241015112315656](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015112315656.png)

> • OSPF域（Domain）：一系列使用相同策略的连续 OSPF网络设备所构成的网络。 
>
> • OSPF路由器在同一个区域（Area）内网络中泛洪LSA。为了确保每台路由器都拥有对网络拓扑的一致认知， LSDB需要在区域内进行同步。

#### OSPF多区域

![image-20241015112518223](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015112518223.png)

> • 区域的分类：区域可以分为骨干区域与非骨干区域。骨干区域即Area0，除Area0以外其他 区域都称为非骨干区域。 
>
> • 多区域互联原则：基于防止区域间环路的考虑，非骨干区域与非骨干区域不能直接相连， 所有非骨干区域必须与骨干区域相连。

#### OSPF路由器类型

![image-20241015112646709](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015112646709.png)

> • 区域内路由器（Internal Router）：该类路由器的所有接口都属于同一个OSPF区域。 
>
> • 区域边界路由器ABR（Area Border Router）：该类路由器的接口同时属于两个以上的区域， 但至少有一个接口属于骨干区域。 
>
> • 骨干路由器（Backbone Router）：该类路由器至少有一个接口属于骨干区域。 
>
> • 自治系统边界路由器ASBR（AS Boundary Router）：该类路由器与其他AS交换路由信息。 只要一台OSPF路由器引入了外部路由的信息，它就成为ASBR。

AS指的是自治系统

#### OSPF单区域&多区域典型组网

![image-20241015112921805](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015112921805.png)

> • 中小型企业网络规模不大，路由设备数量有限，可以考虑将所有设备都放在同一个OSPF区域。 • 大型企业网络规模大，路由设备数量很多，网络层次分明，建议采用OSPF多区域的方式部署。



## 典型配置

进程适用于本台设备上区分启动多个OSPF协议做隔离用的

### OSPF基础配置命令

1.

---

[Huawei]**ospf** [*process-id* | **router-id** *router-id*]

---

*process-id*用于标识OSPF进程，默认进程号为1,。OSPF支持多进程，在同一台设备上可以运行多个不同的OSPF进程，它们之间互不影响。**router-id**用于手工指定设备的ID号。如果没有通过命令指定ID号，系统会从当前接口的IP地址中自动选取一个作为设备的ID号



2.（OSPF视图）创建并进入OSPF区域

---

[Huawei-ospf-1]**area** *area-id*

---

**area**命令用来创建OSPF区域，并进入区域视图。 *area-id*可以是十进制整数或点分十进制格式。采取整数形式时，取值范围是0~4294967295



3.指定运行OSPF的接口

---

[Huawei-ospf1-area-0.0.0.0]**network** *network-address wildcard-mask*

---

**network**用于指定运行OSPF协议的接口和接口所属的区域。*network-address*为接口所在的网段地址。

*wildcard-mask*为IP地址的反码，相当于将IP地址的掩码反转，用来表示**掩码长度**。

> • Router ID的选择顺序是：优先从Loopback地址中选择最大的IP地址作为设备的ID号，如果 没有配置Loopback接口，则在接口地址中选取最大的IP地址作为设备的ID号。



4.配置OSPF接口开销

---

[Huawei-GigabitEthernet0/0/0] **ospf cost** *cost*

---

配置开销，缺省自动计算，cost范围1~65536



5.设置OSPF带宽参考值

---

[Huawei-ospf-1]**bandwidth-reference** *value*

---

**bandwidth-reference** 用来设置通过公式计算接口开销所依据的带宽参考值。取值范围是1~2147483648单位Mb/s，缺省值100.



6.设置接口在选举DR时的优先级

---

[Huawei-GigabitEthernet0/0/0]**ospf dr-priority** *priority*

---

用来设置接口在选举DR时的优先级。值越大，优先级越高 0~255


# 实现VLAN间通信

## 技术背景

### VLAN通信背景

 ![image-20241014195633332](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014195633332.png)

![image-20241014195654945](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014195654945.png)

三层设备要会学习路由。二层设备的特征提供大量接口

## 使用路由器(物理接口、子接口)实现VLAN间通信

### 使用路由器实现VLAN间通信、

#### 使用路由器物理接口

![image-20241014200935756](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014200935756.png)

优点是一个接口对应一个VLAN，如果出现故障的话，只会影响到对应的VLAN信息。



#### 使用路由器子接口

![image-20241014201134050](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014201134050.png)

子接口的好处在于可以只连接一条线，只使用一个端口，这样的话节省线材和空间以及成本。缺点的话是一旦出现物理故障的话，那么所有VLAN都会故障。

#### 子接口处理流程

![image-20241014201332005](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014201332005.png)

#### 子接口配置示例

![image-20241014201356862](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014201356862.png)

第二条命令指的是，如果收到带数据标签是VLAN10的时候，可以关联到这个子接口进行处理

第四条命令是配置了一个arp的广播功能，开启这个功能之后，如果接受过来的是一个arp地址的话，子接口可以去做相应的响应。

## 使用VLANIF技术实现VLAN间通信

三层交换机和VLANIF接口

三层交换机除了具有交换模块，内部还有路由模块，可以实现VLAN之间的通信

VLANIF实际上是一个三层接口，针对这个接口可以配置IP地址，配完之后只要接口状态是UP的，就可以出现直连路由。也是一个虚拟接口。

![image-20241014202642808](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014202642808.png)

### VLANIF配置示例

![image-20241014202840376](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014202840376.png)

配置完ip之后，就会有一个直连路由，10的含义就是如果有vlan10的数据，就可以去处理解析它的。

### VLANIF转发流程

![image-20241014203313818](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014203313818.png)

PC1向外发送的目的MAC地址实际上是MAC地址2，因为PC1->2之间是属于一个不同网段之间的通信，两个VLANIF接口也是有对应的MAC地址，这个地址和设备型号有关，可能不一样。

在路由模块的时候会去掉对应的VLAN信息，然后根据IP地址查找路由表

路由模块会重新封装信息然后转发信息，重新封装会封装数据链路层的内容，修改的是MAC地址，包括VLAN。通过VLAN20的交换层接口到达VLAN20

## 三层通信过程解析

### 网络拓扑

![image-20241014204151920](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014204151920.png)

### 链接逻辑图

![image-20241014204201472](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241014204201472.png)


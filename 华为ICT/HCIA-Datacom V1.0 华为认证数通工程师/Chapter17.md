# 广域网技术

## 早期广域网技术概述

![image-20241018212316044](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018212316044.png)

![image-20241018212436137](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018212436137.png)

### 早期广域网技术介绍

早期广域网与局域网的区别在于数据链路层和物理层的差异性，在TCP/IP参考模型中，和其他各层无异

![image-20241018212654013](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018212654013.png)

![image-20241018212913246](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018212913246.png)

![image-20241018213115610](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018213115610.png)

## PPP协议原理和配置

### PPP协议原理

Proint to Point Protocol 全双工连路上的数据传输 由一系列协议族构成



提供了安全认证协议族PAP和CHAPPassword Authentication P  Challenge Handshake Authentication



提供了良好的扩展性，例如当需要在以太网链路上承载PPP协议时，可以扩展为PPPoE

提供LCP 链路控制协议 链路层进行参数协商，例如最大传输单元LTU



提供各种NCP 网络控制协议 主管网络层 对上的 如IPCP，提供各网络层参数的协商，更好地支持了网络层协议

### PPP链路建立流程

当路由器使用Serial口进行连接且对应的接口状态为UP的时候，会进行以下过程

- 链路层协商：通过LCP报文进行链路参数协商，建立链路层支持
- 认证协商（可选）：通过链路建立阶段协商的认证方式进行链路认证(配置用户名和密码)
- 网络层协商：通过NCP协商来选择和配置一个网络层协议并进行网络层参数协商

当完成以上过程之后，接口对应的协议状态也成为UP 这个接口就可以投入使用了

### PPP链路接口状态机

PPP链路会存在三个状态，在这三个状态分别对应三种接口的状态机

![image-20241022093541859](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241022093541859.png)

我们可以通过状态机的情况来推断到底是哪个步骤或者过程出现了问题

### LCP报文格式

PPP协议可由Protocol字段标识不同类型的PPP报文。例如，当Protocol字段为0xC021时，代表是LCP报文。此时又由Code字段标识不同类型的LCP报文，如

![image-20241022094054031](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241022094054031.png)

LCP报文也会有不同的类型，例如...建立连接时的MTU协商，最大传输单元的多少，或者是是否需要下一步认证，都在information那里显示

PPP的Protocol字段分别有

0x0021:IP报文

0x8021:IPCP报文

0xC021:LCP报文

0xC023:PAP报文

0xC223:CHAP报文

在Information当中的第一个字段是Code 在协议为LCP时，0x01代表是配置请求报文，0x02表示配置成功报文，0x03表示配置参数需要协商 0x04代表配置参数不识别 Configure-Request Configure-ACK Configure-Nak Configure-Reject

在Data部分当中使用的是TLV的架构Type Length Value 这三个字段可以有需要的话就网上增加 所以对于PPP协议扩展性很好 需要新增加就采用一个TLV架构即可

![image-20241022095052121](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241022095052121.png)

### LCP协商过程-正常协商



![image-20241023005244469](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023005244469.png)



### 参数不匹配

![image-20241023005416087](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023005416087.png)

![image-20241023005529959](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023005529959.png)



### PPP认证模式 - PAP

![image-20241023005742105](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023005742105.png)

一次交互 两次握手 只有被认证方的信息在传输

明文发送



### CHAP

![image-20241023010116056](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023010116056.png)

密码不会被发在链路上，只有两端内部进行计算，链路当中传递的是有关密码内容的值



### NCP协商 - 静态IP地址协商

![image-20241023010344959](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023010344959.png)

### 动态IP地址协商

![image-20241023010514950](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023010514950.png)

### PPP基础配置命令

![image-20241023011022195](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023011022195.png)

![image-20241023011032265](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023011032265.png)

### CHAP认证配置命令

![image-20241023011050769](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023011050769.png)

### 配置举例 PAP认证

![image-20241023011115197](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023011115197.png)

### CHAP认证

![image-20241023011135856](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023011135856.png)

## PPPoE原理与配置

### 什么是PPPoE

![image-20241023013737788](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023013737788.png)

### PPPoE应用场景

![image-20241023013932100](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023013932100.png)

### PPPoE报文

![image-20241023014525251](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023014525251.png)

**重点**：报文名称以及相关内容

### PPPoE发现阶段

![image-20241023014808352](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023014808352.png)

### PPPoE会话阶段

![image-20241023014836772](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023014836772.png)

### PPPoE会话终结阶段

![image-20241023014933647](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023014933647.png)

### PPPoE基础配置

![image-20241023015359174](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023015359174.png)

### 配置实例-PPPoE客户端

![image-20241023015427020](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023015427020.png)

### PPPoE服务器端

![image-20241023015558458](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023015558458.png)

### 配置验证

![image-20241023015536212](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023015536212.png)

## 广域网技术的发展

### 传统IP路由转发

![image-20241023091135248](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023091135248.png)

### MPLS标签转发

在路由器的骨干节点定义，使得能够快速且高效的转发报文，是一个封装在数据帧上的标签，可以定义优先级，需要维护对应的类似路由表的MPLS表，根据对应表项可以进行快速且多条同时转发。这些标签既可以静态配置，也可以通过对应的协议动态控制。  只是一个本地标签维护表，不需要知道整个网络每一跳和每一跳之间所有的标签的信息



有隧道的特性 可以应用在VPN当中完成隧道数据转发





#### MPLS转发存在的问题

需要知道整个网络的信息 所有内容需要人员手工配置

动态标签分发的问题 基于原有的IGP分配  提供端到端的一些质量保证，过程需要路由器和路由器之间运行比较复杂的协议来维护质量保证的路径



有没有更好的转发方式呢？有的

### Segment Routing 简介

分段路由

基于现有协议进行扩展，只需要开启IGB之后就可以运行SR协议

引入源路由机制

支持通过控制器集中算路

由业务来定义网络

业务驱动网络，由应用提出需求，控制器收集网络拓扑，带宽利用率，最后根据业务需求计算显式路径



#### 转发原理

SR将路径分成一个个的段，并为这些段分配SID SID的分配对象有两种，转发节点或者临街链路。

![image-20241023113531076](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023113531076.png)

段的序列能决定对应的下一跳和下下跳是什么，在第一台上就已经说明了。

打上完整路径信息知道转发



![image-20241023113729232](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023113729232.png)



NCE所有配置通过NETC传到每一台路由 路径通过PCEP转发



### 应用

可以根据需求来变换不同的路径

![image-20241023113923987](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023113923987.png)




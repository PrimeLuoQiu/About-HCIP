# 网络管理与运维

## 网络管理与运维基本概念

### 网络管理基本功能

OSI定义了五大功能模型：

​	配置管理、性能管理、故障管理、安全管理、计费管理

### 网络管理方式

传统网络管理：人机交互 人通过总机的Web页面控制每一台机器，或者查看告警信息，

​				 机机交互 人通过一个网络管理工作站对所有品牌的设备进行统一管理，使用SNMP

基于iMaster NCE的网络管理

​	有分析 有控制 提供智能化分析 提供一些它觉得可靠的信息 内置AI和大数据

## SNMP原理与配置

### SNMP原理

#### 通过CLI或Web进行管理

- 规模较小时，是常见的管理方式
  - 可以通过HTTP、Telnet、Console方式登录，进行管理
  - 不需要安装任何服务器，成本低
  - 网管自身要求熟练掌握各个网络理论知识以及配置命令
  - 规模较大或拓扑复杂时，局限性大

#### 基于SNMP的集中式管理

是广泛应用于TCP/IP网络的管理标准协议，提供了一种通过运行网络管理软件的中心计算机，级NMS来管理网元的办法。

网管可以利用NMS在网络上的任意节点完成信息查询、信息修改和故障排查等工作，提升效率

屏蔽了不同产品之间的差异，实现了不同种类和厂商的网络设备之间的统一管理

> • SNMP共有三个版本：SNMPv1、SNMPv2c和SNMPv3。 
>
> ​	▫ 1990年5月，RFC 1157定义了SNMP的第一个版本SNMPv1。RFC 1157提供了一种监 控和管理计算机网络的系统方法。SNMPv1基于团体名认证，安全性较差，且返回报 文的错误码也较少。 
>
> ​	▫ 1996年，IETF颁布了RFC 1901，定义了SNMP的第二个版本SNMPv2c。SNMPv2c中 引入了GetBulk和Inform操作，支持更多的标准错误码信息，支持更多的数据类型 （Counter64、Counter32）。 
>
> ​	▫ 鉴于SNMPv2c在安全性方面没有得到改善，IETF又颁布了SNMPv3的版本，提供了基 于USM（User-Based Security Model，用户安全模块）的认证加密和VACM（Viewbased Access Control Model，基于视图的访问控制模型）功能。

#### SNMP典型结构

![image-20241023202028797](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023202028797.png)

为了在SNMP上运行管理进程。每个被管理设备需运行代理进厂，它们利用SNMP报文进行通信。

NMS是一个采用SNMP协议对网络设备进行管理。监控的系统，运行在NMS服务器上

代理进程云星宇被管理设备上，维护被管理设备的信息数据并响应来自NMS的请求，把管理数据汇报发给请求的NMS

> • NMS通常是一个独立的设备，运行网络管理应用程序。网络管理应用程序至少能够提供一 个人机交互界面，网络管理员通过人机交互界面完成绝大多数网络管理工作。比较常见的 人机交互方式为通过Web页面进行交互，即网络管理员通过带显示器的终端，通过 HTTP/HTTPS访问NMS提供的Web页面。

#### SNMP的信息交互

- NMS和被管理设备的信息交互分为两种：
  - NMS通过SNMP协议发送配置信息请求或查询配置信息请求。代理进程根据NMS的请求消息做出响应。
  - 被管理设备可以主动向NMS上报告警信息(Trap)以便网络管理员及时发现故障
- 被管理对象：一个NMS可能包含多个被管理对象，被管理对象可以是设备中的某个硬件，也可以是在硬、软件上配置的参数集合
- SNMP通过MIB去描述可管理实体的一组对象

#### MIB

- 是一个数据库，指明了被管理设备锁维护的变量(即能够被代理进程查询和设置的信息)。MIB在数据库定义了被管理设备的一系列属性
  - 对象标识符(Object IDentifier, OID)
  - 对象的状态
  - 对象的访问权限
  - 对象的数据类型等
- MIB给出了一个数据结构，包含了网络中所有可能的被管理对象的集合。因为数据结构与树类似，MIB又被成为对象命名树

> • MIB的定义与具体的网络管理协议无关。设备制造商可以在产品（如路由器）中包含SNMP 代理软件，并保证在定义新的MIB项目后该软件仍遵守标准。用户可以使用同一网络管理客 户软件来管理具有不同版本MIB的多个路由器。若一台路由器上不支持此MIB，那么就无法 提供相应的功能。 
>
> • MIB可以分为公有MIB和私有MIB两种。 
>
> ▫ 公有MIB：一般由RFC定义，主要用来对各种公有协议进行结构化设计和接口标准化 处理。大多数的设备制造商都需要按照RFC的定义来提供SNMP接口。 
>
> ▫ 私有MIB：是公有MIB的必要补充，当公司自行开发私有协议或者特有功能时，可以 利用私有MIB来完善SNMP接口的管理功能，同时对第三方网管软件管理存在私有协 议或特有功能的设备提供支持。如华为公司企业节点为：1.3.6.1.4.1.2011。

#### 常见MIB节点

![image-20241023204020842](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023204020842.png)

> • MIB节点的最大访问权限表明网管能够通过该MIB节点对设备进行的操作： 
>
> ​	▫ not-accessible：无法进行任何操作。 
>
> ​	▫ read-only：可以读取信息。 
>
> ​	▫ read-write：可以读取信息和修改配置。 
>
> ​	▫ read-create：可以读取信息、修改配置、新增配置和删除配置。 
>
> • 设备在生成告警时，不仅会上报当前发生的告警类型，同时会绑定一些变量。比如当发送 接口linkDown告警时，需要同时绑定接口索引，接口的当前配置状态等变量。 
>
> ​	▫ ifIndex：接口索引（编号） 
>
> ​	▫ ifAdminStatus：管理状态，即接口是否被shutdown：1，undo shutdown；2， shutdown 
>
> ​	▫ ifOperStasuts：接口当前的操作状态，即接口的链路层协议状态：1，Up；2，Down 
>
> ​	▫ ifDesc：接口描述

#### SNMP管理模型

![image-20241023204413137](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023204413137.png)

#### SNMPv1

![image-20241023204438617](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023204438617.png)

> • SNMPv1定义了5种协议操作： 
>
> ​	▫ Get-Request：NMS从被管理设备的代理进程的MIB中提取一个或多个参数值。 
>
> ​	▫ Get-Next-Request：NMS从代理进程的MIB中按照字典式排序提取下一个参数值。 
>
> ​	▫ Set-Request：NMS设置代理进程MIB中的一个或多个参数值。 
>
> ​	▫ Response：代理进程返回一个或多个参数值。它是前三种操作的响应操作。 
>
> ​	▫ Trap：代理进程主动向NMS发送报文，告知设备上发生的紧急或重要事件。

#### SNMPv2

![image-20241023204609967](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023204609967.png)

> • SNMPv2c新增了2种协议操作： 
>
> ​	▫ GetBulk：相当于连续执行多次GetNext操作。在NMS上可以设置被管理设备在一次 GetBulk报文交互时，执行GetNext操作的次数。 
>
> ​	▫ Inform：被管理设备向NMS主动发送告警。与Trap告警不同的是，被管理设备发送 Inform告警后，需要NMS进行接收确认。如果被管理设备没有收到确认信息则会将告警暂时保存在Inform缓存中，并且会重复发送该告警，直到NMS确认收到了该告警或者发送次数已经达到了最大重传次数。

#### SNMP v3

![image-20241023205227918](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023205227918.png)

> • SNMPv3增加了身份验证和加密处理的功能。 
>
> ​	▫ 身份验证：身份验证是指代理进程（NMS）接收到信息时首先必须确认信息是否来自 有权限的NMS（代理进程）并且信息在传输过程中未被改变。 
>
> ​	▫ 加密处理：SNMPv3报文中添加了报头数据和安全参数字段。比如当管理进程发出 SNMPv3版本的Get-Request报文时可以携带用户名、密钥、加密参数等安全参数，代理进程回复Response报文时也采用加密的Response报文。这种安全加密机制特别 适用于管理进程和代理进程之间需要经过公网传输数据的场景。

#### SNMP小节

![image-20241023205303855](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023205303855.png)

### SNMP基本配置

![image-20241023220512252](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220512252.png)

![image-20241023220523302](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220523302.png)

![image-20241023220536379](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220536379.png)

![image-20241023220547371](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220547371.png)

## 基于华为iMaster NCE的网络管理

### 网络产业的变革与挑战

![image-20241023220639272](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220639272.png)

### 华为iMaster NCE

![image-20241023220706427](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220706427.png)

### NETCONF简介

Network Configuration Protocol 提供一套管理网络设备的机制。用户可以使用这套机制增删改网络设备的配置，获取网络设备的配置和状态信息

![image-20241023220821167](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220821167.png)

### NETCONF的优势

![image-20241023220841381](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220841381.png)

### 一次典型NETCONF交互

![image-20241023220859878](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023220859878.png)

### YANG语言描述

Yet Another Next Generation 一种数据建模语言 实现了对NETCONF数据内容的标准化

定义了数据的层次化结构，可用于基于NETCONF的操作。建模对象包括配置、状态数据、远程过程调用和通知。可以对NETCONF客户端和服务器端之间发送的所有数据进行一个完整的描述。

![image-20241023221031467](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023221031467.png)

### YANG和XML

![image-20241023221044903](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023221044903.png)

![image-20241023221053250](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023221053250.png)

### Telemetry基本概述

![image-20241023221121639](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023221121639.png)

### 总结

![image-20241023221131682](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241023221131682.png)
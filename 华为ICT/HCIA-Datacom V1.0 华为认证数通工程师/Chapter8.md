# 以太网链路聚合与交换机堆叠、集群

## 网络可靠性需求

### 网络的可靠性

- 网络的可靠性指当设备或者链路出现单点或者多点故障时保证网络服务不间断的能力
- 网络的可靠性可以从单板、设备、链路多个层面实现。

![image-20241004145552203](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004145552203.png)

### 单板可靠性

![image-20241004145748121](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004145748121.png)

通过交换网板实现网络的交换

这个单板指的是，在主控板的两层当中，一个为主控板，另一个备用，当主控板损坏的时候可以使用备用主控板来进行计算和分配，同时交换网版也会留出来一个空板用来做备用。至于线路板，可以准备一个接口多接二层或者三层的板，已达到链路聚合的效果。如果只接一个的话，会存在单点故障

![image-20241004150111813](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004150111813.png)

![image-20241004152426412](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004152426412.png)

就是上一章节的使用生成树协议

![image-20241004153405544](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004153405544.png)

说白了，是既要又要，又要带宽，还能提供备份的链路、

## 链路聚合技术原理与配置

### 链路聚合基本原理

#### 提升链路带宽

![image-20241004154031725](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004154031725.png)

这样的话虽然很保险，但是存在带宽的浪费，全部堵塞掉之后

#### 以太网链路聚合

Eth-Trunk技术 多个物理接口捆绑成为一个逻辑接口 增加了贷款

![image-20241004154213348](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004154213348.png)

#### 链路聚合基本术语/概念

![image-20241004154300751](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004154300751.png)

创建一个接口生成一个组

进入的都是成员接口 相应的就是成员链路

然后能转发数据的是活动接口对应活动链路 不能的就是非了

限定最多能有几个接口作为活动接口和非活动接口。

### 链路聚合手工模式

应用场景：设备老旧，低端，不支持LACP协议

![image-20241004154735725](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004154735725.png)

#### 手工模式缺陷

![image-20241004154940801](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004154940801.png)

在插拔过程中容易出错，不能保证会不会形成环路等问题 但是当1接口出问题的话，流量还是会进行分担

![image-20241004155100280](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004155100280.png)

对端之间没有协议互通，那么对方接口物理上是up的，但是到转发上或许转发不了。

### 链路聚合LACP模式

#### LACPDU

![image-20241004155341862](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004155341862.png)

协议交互和协议报文

#### 系统优先级

![image-20241004155551120](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004155551120.png)

协议报文互传，确认参照接口，然后根据其它接口的状态。

数值越小越优

#### 接口优先级

![image-20241004205424025](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004205424025.png)

#### 最大活动接口数

![image-20241004205648425](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004205648425.png)

![image-20241004205740115](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004205740115.png)

#### 活动链路选举

![image-20241004205811186](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004205811186.png)

![image-20241004205922745](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004205922745.png)

![image-20241004205949529](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004205949529.png)

#### 负载分担

![image-20241004210028336](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004210028336.png)

数据流：每根链路上负载均衡 速度相对来说比较快 向外发可能是乱序的

第二种相对来说更快。相对来说可能不是乱序的

#### 负载分担模式

![image-20241004210325158](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004210325158.png)

#### 典型使用场景

![image-20241004210430636](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004210430636.png)

![image-20241004210531604](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004210531604.png)

第四种是心跳线。链路捆绑

## 堆叠/集群概述

### 什么是堆叠、集群

![image-20241004210729817](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004210729817.png)

链接的线缆是专门的线缆，并不是双绞线

### 堆叠、集群的优势

![image-20241004210859600](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004210859600.png)

### 实际应用

![image-20241004211206231](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004211206231.png)

![image-20241004211308348](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004211308348.png)

VRRP是网关技术。简化配置。

![image-20241004211403257](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004211403257.png)

## 总结

![image-20241004211541967](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241004211541967.png)


# IPv6基础

## IPv6概述

### IPv6背景及定义

![image-20241024033702592](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024033702592.png)

#### IPv6优势

​	包括无限的地址空间、层次化的地址结构、即插即用、简化的报文头部、安全特性以及移动性

![image-20241024033903574](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024033903574.png)

#### IPv6基本包头

![image-20241024034023440](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024034023440.png)

#### IPv6拓展包头

![image-20241024034155857](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024034155857.png)

通过NextHeader来引出后面是不是还有相关的信息以及包头存在

#### IPv6报文处理机制

![image-20241024034408076](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024034408076.png)

=多少是只要对应的是那个数值，就意味着有对应的拓展包头按需读取

#### IPv6地址

![image-20241024034627986](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024034627986.png)

0写在分段前可以省略，写在分段后省略不了

地址/掩码

有地址有掩码就有子网号 不能分配 但没有广播地址

#### IPv6地址缩写规范

![image-20241024034816802](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024034816802.png)

整个IPv6中只允许有一个::

### IPv6地址分类

#### IPv6地址分类

分为 **单播地址、组播地址和任播地址**

![image-20241024035036847](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035036847.png)

#### IPv6单播地址结构

![image-20241024035111494](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035111494.png)

网络号

接口号 主机号

#### IPv6单播地址接口标识

![image-20241024035242011](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035242011.png)

将MAC地址转换为IPv6接口标识

#### IPv6常见单播地址 GUA

Global Unicast Address 类似于公网IP的

![image-20241024035514595](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035514595.png)

#### IPv6常见单播地址 - ULA

Unique Local Address IPv6私网地址 只能内网使用 节省地址

![image-20241024035716134](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035716134.png)

#### IPv6常见单播地址 LLA

Link-Local Address 链路本地地址

![image-20241024035833538](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035833538.png)

只能本地链路使用 FE80 

单一链路层面通信 发现邻居 只能本链路使用 只能互相通信 每一个接口都必须具备一个本地地址



#### IPv6组播地址

一对多通信

![image-20241024035951440](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024035951440.png)

发给多个人 同一组的都可以收到

#### 被请求节点组播地址

![image-20241024040058682](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024040058682.png)

邻居发现和地址重复检测功能

#### 任播地址

![image-20241024040152678](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024040152678.png)

找最近服务器 访问同一个网页 同一个页面 相同

多个Web服务器提供相同功能的时候，希望终端能够选择最短的路径转发

## IPv6地址配置

### 主机和路由器的IPv6地址

- 一般情况下，主机和路由器的单播IPv6地址以及加入的组播地址如下

![image-20241024062044073](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024062044073.png)

### IPv6单播地址业务流程

一个接口在发送IPv6报文之前要经历地址配置，DAD，地址解析这三个阶段，NDP(Neighbor Discovery Protocol，邻居发现协议)扮演了重要角色。

![image-20241024062707008](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024062707008.png)

### NDP

RFC定义了NDP，该RFC后来被RFC4861取代

NDP使用ICMPv6报文实现其功能

![image-20241024063301222](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024063301222.png)

### IPv6动态地址配置

![image-20241024064504908](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024064504908.png)

RA： Registration Authority 注册审批机构

### DAD

![image-20241024064736106](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024064736106.png)

### 地址解析

![image-20241024064755722](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024064755722.png)

## IPv6典型配置举例

### IPv6基本配置

1.使能IPv6

---

**IPv6**

---

使能设备转发IPv6单播报文，包括本地IPv6报文的发送和接收

---

接口视图 **ipv6 enable**

---

2.配置接口的链路本地地址

---

接口视图

**ipv6 address** *ipv6-address* **link-local**

**ipv6 address auto link-local**

---

在接口视图下，通过手工或者自动的方式，配置接口的链路本地地址

3.配置接口的全球单播地址

---

**ipv6 address** { *ipv6-address prefix-length | ipv6-address | prefix-length* }

**ipv6 address auto** { **global** | **dhcp** }

---

在接口视图下，通过手工或者自动(有状态或无状态)的方式，配置接口的全球单播地址

4.配置IPv6静态路由

---

**ipv6 route-static** *dest-ipv6-address prefix-length* { *interface-type interface-number* [ *nexthop-ipv6-address* ] | *nexthop-ipv6-address* } [ **preference** *preference*]

---

5.查看接口的IPv6信息

---

**display ipv6 interface** [ *interface-type interface-number | **breif** ]

---



6.查看邻居表项信息

---

**display ipv6 neighbors**

---



7.使能系统发布RA报文功能

---

接口视图

**undo ipv6 nd ra halt**

---

默认情况下，华为路由器接口不发送ICMPv6 RA报文，则该接口所连链路上的其他设备无法进行无状态地址自动配置。若想进行IPv6无状态地址配置，需要手动开启发送RA报文



### 配置一个小型IPv6网络

![image-20241024070128378](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024070128378.png)

![image-20241024070140310](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024070140310.png)

![image-20241024070152970](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024070152970.png)

![image-20241024070201550](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024070201550.png)

## 本章总结

![image-20241024070217452](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241024070217452.png)






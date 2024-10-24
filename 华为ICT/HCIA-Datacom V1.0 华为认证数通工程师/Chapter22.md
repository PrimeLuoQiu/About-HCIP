# 园区网络典型组网架构及案例实践

## 园区网络基本概念

### 什么是园区网

底层技术是802.3协议族和802.11 有线和无线

在一定范围之内使用局域网叫做一个园区网

![image-20241025000111659](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025000111659.png)

分模块设计

三层构架 DMZ区域核心服务器 管理、安全属于软件层面

对于外部来说，园区网络会有两种网络接入，一种是园区网访问因特网，会有因特网的连接，还会有大型公司的分支结构的概念，这个时候就需要用专线MPS和VPN这些分支机构进行互联 当有人在外部想要访问内部园区的话，就要使用因特网搭建一个VPN访问进来



云计算 内部数据中心，一般是本地的，当链路出现故障，就没有办法正常的对外部客户提供服务 可以选择在公有云上买一些服务 通过Internet与之相连，实现当本地数据中心中断之后，那么私有云和公有云可以对外提供业务

### 园区网络典型架构

![image-20241025001016910](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001016910.png)

### 小型园区网络典型架构

![image-20241025001114207](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001114207.png)

### 中型园区网络典型架构

![image-20241025001203717](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001203717.png)

数据中心区域和DMZ区域，出口层也没有很多设备，也没有分支机构，一般叫做中型园区网络

### 大型园区网络典型架构

![image-20241025001345483](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001345483.png)

### 园区网络主要协议/技术

![image-20241025001426807](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001426807.png)

## 典型园区网络建设流程

![image-20241025001651384](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001651384.png)



### 园区网络项目生命周期

![image-20241025001751885](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001751885.png)

> • 网络的规划与设计是一个项目的起点，完善细致的规划工作将为后续的项目具体工作打下 坚实的基础。 
>
> • 项目实施是工程师交付项目的具体操作环节，系统的管理和高效的流程是确保项目实施顺 利完成的基本要素。 
>
> • 要保证网络各项功能正常运行、从而支撑用户业务的顺利开展，需要对网络进行日常的维 护工作和故障处理。 
>
> • 用户的业务在不断发展，因此用户对网络功能的需求也会不断变化。当现有网络不能满足 业务需求，或网络在运行过程中暴露出了某些隐患时，就需要通过网络优化来解决。

### 小型园区网络设计

![image-20241025001834216](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001834216.png)

组网考虑拓扑和设备类型 网络设计要考虑二层的环路和可靠性 以及如果有AP带来的WLAN设计 出口就要考虑安全 运维就要考虑网管和智能运维



### 组网方案设计

![image-20241025001957669](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025001957669.png)

> • 综合考虑预算、业务需求等因素之后，物理拓扑如上图所示。 
>
> • 整个网络采用三层架构 
>
> ​	▫ 接入层接入交换机采用S3700，为员工PC以及打印机等终端提供百兆网络接入。 
>
> ​	▫ 汇聚层采用S5700设备，作为二层网络的网关。 
>
> ​	▫ 核心&出口采用AR2240设备，作为整个园区网络的出口。 
>
> • 注：Agg为Aggregation的缩写，表示汇聚层设备。Acc为Access的缩写，表示接入层设备。

### 基础业务设计：VLAN设计

![image-20241025002111406](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002111406.png)

### VLAN规划

![image-20241025002131446](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002131446.png)

### 基础业务设计：IP地址设计

![image-20241025002213365](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002213365.png)

互联IP地址推荐使用**30**位掩码的IP地址，核心设备使用主机地址 较小的IP地址。

### IP地址规划

![image-20241025002257042](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002257042.png)

### 基础业务设计：IP地址分配方式设计

![image-20241025002318635](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002318635.png)

终端用户的IP地址分配，建议采用**DHCP**方式，由网关设备提供DHCP服务。

>• IP地址分配时可以使用动态IP分配或者静态IP绑定。在中小型园区中， IP地址具体的分配原 则如下： 
>
>• 出口网关设备： WAN侧接口的IP地址由运营商进行分配，可以通过静态IP地址、 DHCP、 或者PPPoE方式分配，对于出口网关的IP地址需要提前与运营商沟通获取。 
>
>• 服务器、特殊终端设备（打卡机、打印服务器、 IP视频监控设备等）建议采用静态IP地址 绑定方式分配。 
>
>• 用户终端：用户办公用PC、IP电话等设备建议通过在网关设备上部署DHCP Server后，统一 通过DHCP方式动态分配。

### IP地址分配方式规划

![image-20241025002418861](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002418861.png)

### 基础业务设计：路由设计

![image-20241025002444755](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002444755.png)

> • 中小型园区网络的路由设计包括园区内部的路由设计及园区出口与Internet/广域设备之间 的路由设计。 
>
> • 园区内部的路由设计：主要满足园区内部设备/终端的互通需求，并且可以与外部路由交互。 由于中小型园 区的网络规模比较小，网络结构也比较简单。 
>
> ​	▫ AP设备：通过DHCP分配IP地址后默认会生成一条缺省路由。 
>
> ​	▫ 交换机、网关设备：通过静态路由即可满足需求，无需部署复杂的路由协议。 
>
> • 园区出口的路由设计：出口路由设计主要满足园区内部用户访问Internet和广域网的需求。 出口设备与 Internet或者WAN连接时，建议在出口设备上配置静态路由来满足需求。

### WLAN设计

![image-20241025002527111](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002527111.png)

> • 除了要规划组网和数据转发方式外，仍需进行： 
>
> ​	▫ 网络覆盖设计：针对无线网络覆盖的区域设计规划，保证区域覆盖范围内的信号强度 能满足用户的要求，并且解决相邻AP间的同频干扰问题。 
>
> ​	▫ 网络容量设计：根据无线终端的带宽要求、终端数目、并发率、单AP性能等数据来设 计部署网络所需的AP数量，确保无线网络性能可以满足所有终端的上网业务需求。 
>
> ​	▫ AP布放设计：在网络覆盖设计的基础上，根据实际情况对AP的实际布放位置、布放 方式和供电走线原则进行修正确认。 
>
> ​	▫ 此外还需进行WLAN安全设计、漫游设计等，本课程不再一一列举。

### WLAN数据规划

![image-20241025002604941](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002604941.png)

### 可靠性设计

![image-20241025002619965](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002619965.png)

### 二层环路避免

![image-20241025002635240](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002635240.png)

### 出口NAT设计

![image-20241025002657689](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002657689.png)

> • 静态NAT适用于有较多静态IP且有客户端需要使用固定IP地址的场景。 
>
> • 动态NAT拥有地址池概念，取地址池中可用地址给客户端访问Internet使用。 
>
> • NAPT在动态NAT的基础上对端口也进行转换，提高公网地址利用率。 
>
> • Easy IP 适用于网络出接口地址动态场景。

### 安全设计

![image-20241025002734938](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002734938.png)

> • 允许部门之间的流量互访，但不允许访问Internet 
>
> • 访客可以访问Internet但不能访问园区内部网络。 
>
> • 可以用过traffic-policy、traffic-filter等技术完成内外网隔离，通过NAT控制内部网络访问 Internet。 
>
> • 在园区网中，经常会出现有员工私接带DHCP的无线路由器，导致内网地址混乱，出现地址 冲突、无法上网等情况。 
>
> • 一般会在接入交换机使能DHCP Snooping防止这种情况。 
>
> • 说明：本案例的安全设计仅依靠路由器或交换机设备实现。

### 运维管理设计

![image-20241025002810787](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002810787.png)

### 小型园区网络部署与实施

![image-20241025002842563](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002842563.png)

### 配置方案

![image-20241025002858325](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002858325.png)

![image-20241025002908079](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002908079.png)

![image-20241025002919750](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002919750.png)

![image-20241025002929921](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002929921.png)

![image-20241025002939652](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002939652.png)

![image-20241025002947668](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002947668.png)

![image-20241025002957560](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025002957560.png)

### 小型园区网络调试

![image-20241025003012042](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025003012042.png)

### 小型园区网络运维

![image-20241025003024818](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025003024818.png)

### 小型园区网络优化

![image-20241025003039817](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025003039817.png)

## 本章总结

![image-20241025003055773](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241025003055773.png)


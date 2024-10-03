# VLAN原理与配置

## 什么是VLAN

在传统以太网当中会因为IP地址的分布出现类似 当主机和交换机较多的时候，就会出现很多不必要的泛洪以及垃圾流量，于是就要应用到VLAN技术



![image-20241001152849926](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001152849926.png)

隔离了广播域

## VLAN的基本概念

### VLAN的基本概念

给数据打上一个特殊的标签让交换机进行识别

![image-20241001153252391](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001153252391.png)

大概是加在MAC地址后面的VLAN标签

![image-20241001155026062](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001155026062.png)

TPID是用来标识这个VLAN协议的**(0x8100)**

PRI代表数据的优先级，数值越低优先级越高

CFI用来判断对应的格式是否标准

VLANID就是我们给他赋予的VLAN值，可以是0-4095 但由于0和4095要保留不能用，所以范围是1-4094

交换机打上对应的VLAN标签 VLAN影响只发生在交换机上。对用户数据没有任何操作。

### VLAN的划分方式

基于接口(缺点：当用户插错接口的时候可能会被分到错误的VLAN) 、 基于MAC地址 、 基于IP子网 、 基于协议 、 基于策略划分(根据上述三种排列组合而来)

#### 基于接口的VLAN划分

![image-20241001155704074](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001155704074.png)

![image-20241001160025011](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001160025011.png)

这个优先级要高于端口的VLAN划分。

对于不同的设备之间，需要使用不同的端口，端口的类型分为三种，分别是 Access 、 Trunk 、Hybrid三种接口。

Trunk是为了让VLAN通过，不需要进行配置 Access是需要打标签的接口 Hybrid是一种混合接口

#### Access接口

![image-20241001160457534](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001160457534.png)

接受的时候，没有标签就打上，有标签就进行判断，如果一样的话就通过，不一样的话就丢弃

发送的时候，根据对应端口的VLAN标签，一样的话删除标签，不一样的话则不管。

#### Trunk接口

![image-20241001160900931](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001160900931.png)

道理和Access接口类似，如果在接收的时候，是一个没标记的，那么就要打上对应的接口所对应的ID，然后进入交换机，如果和交换机端口的ID一样，那么直接进入。

发送的时候，如果和端口一样的ID，那么发送出去的时候就脱掉这个ID，如果不一样，那么就带着它自己的ID一起走。



实例

![image-20241001161727093](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001161727093.png)

可以理解一下

#### Hybrid接口

![image-20241001161710932](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001161710932.png)

![image-20241001162019305](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001162019305.png)

主要应用在以上场景 PC1要独立和服务器通信 PC2也要独立和服务器通信，但PC1和2之间是不能通信的。

![image-20241001162326177](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001162326177.png)

## VLAN的应用

### VLAN的规划

![image-20241001163948518](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001163948518.png)

VLAN编号建议连续分配，以保证VLAN资源合理利用。最常用的划分方式是基于接口的方 式。

 • VLAN分配原则 

​	▫ 按业务规划：可分为语音、视频和数据。

​	▫ 按部门规划：可分为工程部、市场部、财经部等。 

​	▫ 按应用规划：可分为服务器、办公、教室等。

 • VLAN分配技巧 VLAN ID的分配在有效范围内，可以随意分配和选取，但是 为了提高VLAN ID的连续性，可以采用VLAN ID和子网关联 的方式进行分配。

![image-20241001164049373](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001164049373.png)

![image-20241001164103254](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241001164103254.png)

按照细分到每一个IP或每一组IP的情况分成端口和MAC划分

## VLAN的配置示例

### 1.创建VLAN

***

[Huawei] **vlan** *vlan-id*

***

创建并进入VLAN视图，存在直接进入 取值范围1-4094

***

[Huawei] **vlan batch** {*vlan-id1* [**to** *vlan-id2*]}

***

批量创建VLAN 1 - 2

> vlan命令用来创建VLAN并进入VLAN视图，如果VLAN已存在，直接进入该VLAN的视图。
>
>  • undo vlan用来删除指定VLAN。
>
>  • 缺省情况下，将所有接口都加入到一个缺省的VLAN中，该VLAN标识为1。
>
> ​	 ▫ 命令：
>
> ​		 ▫ vlan vlan-id 
>
> ​			▪ vlan-id：指定VLAN ID。整数形式，取值范围是1～4094。
>
> ​		 ▫ vlan batch { vlan-id1 [ to vlan-id2 ] } 
>
> ​			▪ batch：指定批量创建VLAN。
>
> ​			▪ vlan-id1 to vlan-id2：指定批量创建的VLAN ID，其中：
>
> ​				 − vlan-id1表示第一个VLAN的编号。
>
> ​				 − vlan-id2表示最后一个VLAN的编号。vlan-id2的取值必须大于等于vlanid1，它与vlan-id1共同					确定一个VLAN范围。
>
> ​			▪ 如果不指定to vlan-id2参数，则只创建vlan-id1所指定的VLAN。
>
> ​			▪ vlan-id1和vlan-id2是整数形式，取值范围是1～4094。

### Access接口的基础配置命令

#### 1.配置接口类型

***

[Huawei-GigabiteEthernet0/0/1]**port link-type access**

***

接口视图下，配置接口的链路类型为access

#### 2.配置Access接口的缺省VLAN(默认为1)

***

[Huawei-GigabiteEthernet0/0/1]**port default vlan** *vlan-id*

***

配置接口的缺省VLAN并同时加入这个VLAN vlan-id是指缺省VLAN的编号 取值 1-4904

### Trunk接口的基础配置命令

#### 1.配置接口类型

***

[Huawei-GigabiteEhternet0/0/1]**port link-type trunk**

***

配置链路类型

#### 2.配置Trunk接口加入指定VLAN

***

[Huawei-GigabiteEthernet0/0/1]**port trunk allow-pass vlan** {{*vlan-id1* [**to** *vlan-id2*] } | **all**}

***

配置Trunk类型接口加入的VLAN

#### 3(可选).配置Trunk接口的缺省VLAN

***

[Huawei-GigabitEthernet0/0/1]**port trunk pvid vlan** *vlan-id*

***

配置Trunk类型接口的缺省VLAN

> • 命令：port trunk allow-pass vlan { { vlan-id1 [ to vlan-id2 ] | all } 
>
> ​	▫ vlan-id1 [ to vlan-id2 ]：指定Trunk类型接口加入的VLAN，其中：
>
> ​		 ▪ vlan-id1表示第一个VLAN的编号。
>
> ​		 ▪ to vlan-id2表示最后一个VLAN的编号。vlan-id2的取值必须大于等于vlan-id1 的取值。
>
> ​		 ▪ vlan-id1和vlan-id 2为整数形式，取值范围是1～4094。
>
> ​	▫ all：指定Trunk接口加入所有VLAN。
>
>  • 命令：port trunk pvid vlan vlan-id，设置Trunk类型接口的缺省VLAN。
>
> ​	▫ vlan-id：指定Trunk类型接口的缺省VLAN编号。整数形式，取值范围是1～4094。

### Hybrid接口的基础配置命令

#### 1.配置接口类型

***

[Huawei-GigabitEthernet0/0/1]**port link-type hybrid**

***

#### 2.配置Hybrid接口加入指定VLAN

***

[Huawei-GigabitEthernet0/0/1]**port hybrid untagged vlan** {{*vlan-id1*[**to** *vlan-id2*]} | **all**}

***

接口视图下，配置Hybrid类型接口加入的VLAN，这些VLAN的帧以Untagged方式通过接口

***

[Huawei-GigabitEthernet0/0/1]**port hybrid tagged vlan** {{*vlan-id1*[**to** *vlan-id2*]} | **all**}

***

#### 3.配置Hybrid接口的缺省VLAN

***

[Huawei-GigabitEthernet0/0/1]**port hybrid pvid vlan** *vlan-id*

***

接口视图下，配置Hybrid类型接口的缺省VLAN

> • 命令：port hybrid untagged vlan { { vlan-id1 [ to vlan-id2 ] } | all } 
>
> ​	▫ vlan-id1 [ to vlan-id2 ]：指定Hybrid类型接口加入的VLAN，其中：
>
> ​		 ▪ vlan-id1表示第一个VLAN的编号。
>
> ​		 ▪ to vlan-id2表示最后一个VLAN的编号。vlan-id2的取值必须大于等于vlan-id1 的取值。
>
> ​		 ▪ vlan-id1和vlan-id 2为整数形式，取值范围是1～4094。
> ​	▫ all：指定Hybrid接口加入所有VLAN。
>
>  • 命令：port hybrid tagged vlan { { vlan-id1 [ to vlan-id2 ] } | all } 
>
> ​	▫ vlan-id1 [ to vlan-id2 ]：指定Hybrid类型接口加入的VLAN，其中：
>
> ​		 ▪ vlan-id1表示第一个VLAN的编号。
>
> ​		 ▪ to vlan-id2表示最后一个VLAN的编号。vlan-id2的取值必须大于等于vlan-id1 的取值。
>
> ​		 ▪ vlan-id1和vlan-id 2为整数形式，取值范围是1～4094。
>
> ​	 ▫ all：指定Hybrid接口加入所有VLAN。
>
>  • 命令：port hybrid pvid vlan vlan-id，设置Hybrid类型接口的缺省VLAN。
>
> ​	 ▫ vlan-id：指定Hybrid类型接口的缺省VLAN编号。整数形式，取值范围是1～4094
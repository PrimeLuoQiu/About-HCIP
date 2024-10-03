# 华为VRP系统基础

## 华为VRP系统概述

### VRP概念

#### 什么是VRP

华为公司数据通信产品的通用操作系统平台

VRP功能：

- 实现统一的用户界面和管理界面

- 实现控制平面功能，并定义转发平面接口规范

- 实现各产品转发平面与VRP控制平面之间的交互

- 屏蔽各产品链路层对网络层的差异

![image-20240927150229991](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927150229991.png)

#### 文件系统

文件系统是指对存储器中文件、目录的管理

分为

- 系统软件：是设备启动、运行的必备软件。常见的文件后缀名为.cc
- 配置文件：是用户将配置命令保存的文件。常见文件后缀：.cfg .zip .dat
- 补丁文件：是一种与设备系统软件兼容的软件，用于后续系统更新打的补丁包 .pat
- PAF文件： .bin



#### 存储设备

![image-20240927150854463](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927150854463.png)

![image-20240927150955887](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927150955887.png)

### 设备管理方式

分为两种 Web网管方式和 命令行方式

#### Web网管

类似图形化界面，只需要在对应内容当中填入必须的参数即可，例如家里的路由器配置SSID。很直观

#### 命令行方式

可实现对设备的精细化管理，要求熟悉命令行，通过telnet http ssh方式登录。Console口  故障反馈更直接，处理更方便

#### 用户界面

Console界面 只需要让设备和对应的设备用Console口相连，然后使用串口本地访问即可

VTY(远程登录) 要事先配置对应的VTY界面以及对应的功能等。

![image-20240927151836344](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927151836344.png)

![image-20240927152113264](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927152113264.png)

![image-20240927152303391](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927152303391.png)

![image-20240927153215574](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927153215574.png)

![image-20240927153946204](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927153946204.png)

## 命令行基础

命令都有一般格式
$$
命令字+关键字+参数名+参数值
$$
例如

display ip interface GE0/0/0

就是对应的内容

### 命令行视图

用户->系统->接口/协议视图

![image-20240927164408021](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927164408021.png)

### 编辑命令行

BackSpace Ctrl+B === <- Ctrl+A === ->

可以不完整关键字输入 可以使用tab键补全 帮助 ？

![image-20240927192605327](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927192605327.png)

![image-20240927192623316](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927192623316.png)

![image-20240927192700382](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20240927192700382.png)

### 常见文件系统操作命令

pwd 显示当前目录

dir  [/all] [filename | directory]

more [/binary] filename [offset] [all] 用来查看文本文件的具体内容

cd

mkdir

> VRP基于文件系统来管理设备上的文件和目录。在管理文件和目录时，经常会使用一些基本 命令来查询文件或者目录的信息，常用的命令包括pwd，dir [ /all ] [ filename | directory ] 和more [ /binary ] filename [ offset ] [ all ]。 
>
> ▫ pwd命令用来显示当前工作目录。
>
> ▫ dir [ /all ] [ filename | directory ]命令用来查看当前目录下的文件信息。 
>
> ▫ more [ /binary ] filename [ offset ] [ all ]命令用来查看文本文件的具体内容。 
>
> ▫ 本例中，在用户视图中使用dir命令，可以查看flash中的文件信息。
>
>  • 目录操作常用的命令包括：cd directory，mkdir directory和rmdir directory。
>
> ▫ cd directory命令用来修改用户当前的工作目录。
>
> ▫ mkdir directory命令能够创建一个新的目录。目录名称可以包含1-64个字符。

rmdir 只有空目录才能被删除

copy source-filename destination-filename 可以复制文件 若存在，会提示此文件将被替换。且不能和系统启动文件同名

move 只适用于在统一存储设备中移动文件

rename old-name new-name

delete 用来删除文件 可跟参数[/unreserved] [/force]{filename / deviccename}不带un 被移动到回收站 回收站中可通过undelete回复，如果执行delete指定了un 责备永久删除 添加/force 不会给出任何提示信息 devicename指出存储设备的名称

reset recycle-bin [filename/devicename]用来永久删除回收站中的文件

### 基本配置命令

sysname

clock timezone time-zone-name {add|minus} offset 用来对本地时区信息进行设置

clock datetime [utc] HH:MM:SS YYYY-MM-DD 用来设定设备当前或UTC日期和时间

clock daylight-saving-time 用来设置设备的夏令时

> 为了保证与其他设备协调工作，需要准确设置系统时钟。系统时钟的=UTC（Coordinated Universal Time）+当前时区与UTC的时间差，一般设备上都会有内置的UTC和时间差配置。 
>
> ​	▫ 可以通过clock datetime命令直接设置设备的系统时钟，格式为HH:MM:SS YYYYMM-DD，此时UTC等于系统时钟-时间差。 ▫ 也可以通过修改UTC和系统当前时区来修改系统时钟 
>
>  ▪ clock datetime [ utc ] HH:MM:SS YYYY-MM-DD用来修改UTC时间。 
>
> ▪ clock timezone time-zone-name { add | minus } offset 用来配置本地时区信 息。
>
> 本地时间加上或减去offset即为UTC。 
>
> ▫ 有的地区实行夏令时制，因此当进入夏令时实施区间的一刻，系统时间要根据用户的 设定进行夏令时时间的调整。VRP支持夏令时功能。

3.配置命令等级

**command-privilege level** *level* **view** *view-name command-key* 

用来设定指定视图内的命令的级别 级别分为 参观、监控、配置、管理四个级别 分别对应标识 0 1 2 3

4.配置用户通过Password方式登录设备

**user-interface vty 0 4**

[Huawei-ui-vty0-4]**set authentication password cipher** *information*

用来进入指定的用户视图并配置用户认证方式为password 系统支持VTY和Console两种页面 默认状态下，设备一般最多支持15个用户同时通过VTY方式访问

5.配置用户界面参数

***

**idle-timeout** *minutes* [seconds]

***

用来设置用户界面断开连接的超时时间。如果用户在一段时间内没有输入命令。系统将断开连接。缺省情况下，超时时间10分钟

> 虚拟类型终端（Virtual Type Terminal）是一种虚拟线路 端口，用户通过终端与设备建立Telnet或SSH连接后，也就建立了一条VTY，即用户可以通 过VTY方式登录设备。设备一般最多支持15个用户同时通过VTY方式访问。执行userinterface maximum-vty number 命令可以配置同时登录到设备的VTY类型用户界面的最大 个数。如果将最大登录用户数设为0，则任何用户都不能通过Telnet或者SSH登录到路由器。 display user-interface 命令用来查看用户界面信息。

6.配置接口IP地址

***

**interface** *interface-number*

[Huawei-interface-number]**ip address** *ip address*

***

7.查看当前运行的配置文件

***

<Huawei>**display current-configuration**

***

8.配置文件保存

***

<Huawei> Save

***

9.查看保存的配置

***

<Huawei>display save-configuration

***

> • 要在接口运行IP服务，必须为接口配置一个IP地址。一个接口一般只需要一个IP地址,如果接 口配置了新的主IP地址，那么新的主IP地址就替代了原来的主IP地址。
>
>  • 用户可以利用ip address ip-address { mask | mask-length } 命令为接口配置IP地址，这个 命令中，mask代表子网掩码，如255.255.255.0，mask-length 代表的是掩码长度，如24。 这两者任取其一均可。
>
>  • Loopback接口是一个逻辑接口，可用来虚拟一个网络或者一个IP主机。在运行多种协议的 时候，由于Loopback接口稳定可靠，所以也可以用来做管理接口。
>
>  • 在给物理接口配置IP地址时，需要关注该接口的物理状态。默认情况下，华为路由器和交换 机的接口状态为up；如果该接口曾被手动关闭，则在配置完IP地址后，应使用undo shutdown打开该接口。

10.清除已保存的配置

***

<Huawei> **reset saved-configuration**

***

11.查看系统启动配置参数

***

<Huawei> **display startup**

***

用来查看设备本次及下次启动相关的系统软件、备份系统软件、配置文件、License文件、补丁文件及语音文件

12.配置系统下次启动时使用的配置文件

***

<Huawei> **startup saved-configuration** *configuration-file*

***

设备升级时，可以通过此命令让设备下次启动时加载指定的配置文件

13.配置设备重启

***

**reboot**

***

> • reset saved-configuration命令用来清除配置文件或配置文件中的内容。执行该命令后，如 果不使用命令startup saved-configuration重新指定设备下次启动时使用的配置文件，也不 使用save命令保存当前配置，则设备下次启动时会采用缺省的配置参数进行初始化。
>
>  • display startup命令用来查看设备本次及下次启动相关的系统软件、备份系统软件、配置文 件、License文件、补丁文件以及语音文件。
>
>  • startup saved-configuration configuration-file 命令用来指定系统下次启动时使用的配置 文件，configuration-file参数为系统启动配置文件的名称。
>
>  • reboot命令用来重启设备，重启前提示用户是否保存配置。
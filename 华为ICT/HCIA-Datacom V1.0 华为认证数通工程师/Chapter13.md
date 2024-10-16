# AAA原理与配置

提升安全性 查看身份信息，拿到不同权限，再发送

## AAA概述

### AAA概述

包括 Authentication(认证)、Authorization(授权)、Accounting(计费)

这里的计费指的是记录用户去访问的一些网页或者去访问的资源。根据访问的记录和资源进行计费



### AAA常见架构

包括用户、NAS(Network Access Server)、AAA服务器(AAA Server)。

NAS可以是路由、防火墙等设备

![image-20241016162416112](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016162416112.png)

### 认证(Authentication)

支持的认证方式有：不认证、本地认证、远端认证

![image-20241016162842602](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016162842602.png)

不认证就是不认证啦~只要能连上就能访问网络

本地认证类似在路由器当中存入一个数据库，在路由器上进行用户名和密码的校验。

远端认证指的是路由器作为一个传输设备存在，在远端有一个专门用来做认证的AAA服务器对用户名和密码进行校验



本地认证相对来说速度会更快，但是如果全都用本地认证，那么路由器的速率会收到一定的影响，而且一旦路由器出故障了，那么就意味着无法进行认证，所有用户都不能接入互联网

而远端认证的话，对于服务器来讲，专门的设备做专门的工作，那么性能肯定会更好，而且能应付大量用户登录的一个计算。而且同时可以再设置一个备份的服务器，由服务器进行主要认证，当服务器出故障的时候路由器可以再顶上来。



### 授权(Authorization)

同样支持 不授权、本地授权、远端授权

授权信息包括 所属用户组、所属VLAN、ACL编号等

![image-20241016163535750](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016163535750.png)

可以访问互联网，或者访问某个网段，在服务器当中进行存储。授权功能，用户1，可以访问哪些资源

单个授权工作量大 属于某个用户组 然后统一设置某种权限。





### 计费(Accounting)

- 用于监控授权用户的网络行为和网络资源的使用情况
- 支持的计费方式有：不计费、远端计费

根据访问的资源 收费情况是不一样 只记录访问的情况

根据服务器来记录具体访问到了哪些资源

![image-20241016164244676](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016164244676.png)

### AAA实现协议-RADIUS

![image-20241016165413462](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016165413462.png)

使用UDP协议 1812号端口

### AAA常见应用场景

![image-20241016165543314](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016165543314.png)

## AAA配置实现

1.进入AAA视图

---

[Huawei]aaa

---

从系统进入aaa视图进行配置

2.创建认证方案

---

[Huawei-aaa] **authentication-scheme** *authentication-scheme-name*

---

创建认证方案并进入相应的认证方案视图

---

[Huawei-aaa-authentication-scheme-name] **authentication-mode** { **hwtacacs|local|radius**}

---

配置认证方式，local指定认证方式为本地认证。缺省情况下，认证方式为本地认证



hw是华为的认证方式，和radius类似，但hw的认证和授权是分开的，且使用TCP协议



3.创建domain并绑定认证方案

---

[Huawei-aaa]**domain** *domain-name*

---

创建domain并进入相应的domain视图

---

[Huawei-aaa-domain-name]**authentication-scheme** *authentication-scheme-name*

---

在相应的domain视图下绑定认证方案



4.创建用户

---

[Huawei-aaa]**local-user** *user-name* **password cipher** *password*

---

创建本地用户，并配置本地用户的密码

- 如果用户名中带域名分隔符，如@，则认为@前面的部分是用户名，后面部分是域名
- 如果没有@，则整个字符串为用户名，域为默认域



5.配置用户接入类型

---

[Huawei-aaa]**local-user user-name service-type** {{ **terminal|telnet|ftp|snmp|http** }}

---

设置本地用户的接入类型。缺省情况下，本地用户关闭所有的接入类型

当设置了对应的用户名密码并配置了接入类型之后，如果更换接入类型还使用之前的用户名和密码，是不会进行接入的





6.配置用户级别

---

[Huawei-aaa]**local-user** *user-name* **privilege level** *level*

---

指定本地用户的权限级别



当用户Telnet到路由器上时，并且输入了用户名和密码之后，登录了，就可以在路由器上查看用户在线的信息了，以及一些对应的用户信息在本地都是有记录的。可以通过MAC和IP信息找到对应的主机和用户的。



并不是所有人都可以进行访问，每个人接入之后的权限是不一样的，接入进来之后，这些访问的记录也是会被记录下来的。后期可以去做数据的追溯。
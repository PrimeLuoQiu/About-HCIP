# 网络服务与应用

## 文件传输

### FTP

在Web网络还没出现之前，主要使用ftp和tftp进行文件之间的互相传输。

#### FTP基本概念

采用典型的C/S架构，建立TCP链接、两种传输模式：Binary和ASCII模式。

#### FTP传输模式：主动模式

用20端口建立的是数据通道

![image-20241017104319878](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017104319878.png)

#### FTP传输模式-被动模式

![image-20241017105256049](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017105256049.png)

#### 配置命令介绍-设备作为服务器

1.开启FTP服务器端功能

---

[Huawei]**ftp [ipv6] server enable**

---

缺省情况下，设备的FTP服务器端功能是关闭的

2.配置FTP本地用户

---

[Huawei]**aaa**

[Huawei]**local-user** *user-name* **password irreversible-cipher** *password*

[Huawei]**local-user** *user-name* **privilege level** *level*

[Huawei]**local-user** *user-name* **service-type ftp**  需要什么写什么，写什么生效什么

[Huawei]**local-user** *user-name* **ftp-directory** *directory*

---

必须将用户级别配置在3级或者3级以上，否则FTP连接将无法成功

#### 设备作为客户端

![image-20241017105845002](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017105845002.png)

![image-20241017110018072](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017110018072.png)

### TFTP

![image-20241017110225686](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017110225686.png)

#### TFTP传输示例

![image-20241017112500612](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017112500612.png)

这个ACK是应用层上的，并不是UDP回去

#### 配置命令介绍

![image-20241017112614690](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017112614690.png)

## Telnet

### Telnet应用场景

![image-20241017112835975](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017112835975.png)

#### 虚拟用户界面

![image-20241017112955932](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017112955932.png)

### 配置命令介绍

![image-20241017113452362](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017113452362.png)

ssh如果被人抓包了是密文，而Telnet默认是明文的操作

![image-20241017113530828](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017113530828.png)

#### 配置示例

![image-20241017113554680](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017113554680.png)

![image-20241017113611946](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017113611946.png)

## DHCP

 手动配置存在太多的问题，如参数多，难理解、工作量大、利用率低、灵活性差等问题，所以能够动态分配的话会好很多。自动完成

![image-20241017114126145](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017114126145.png)

### 优点

统一管理、地址租期

统一配置地址属于同一个范围。到服务时间节点的话会固定访问是否要继续使用、合理规划

### DHCP工作原理

![image-20241017114554987](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017114554987.png)

 ### 租期更新

![image-20241017114710386](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017114710386.png)



### 配置命令介绍

![image-20241017115305109](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017115305109.png)

![image-20241017115404165](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017115404165.png)

#### 全局配置

![image-20241017115452837](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017115452837.png)

### DHCP接口地址池配置

![image-20241017115717506](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017115717506.png)

![image-20241017115853832](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017115853832.png)

## HTTP

### 使用浏览器访问网址

![image-20241017120315799](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017120315799.png)

### 诞生背景

![image-20241017120227143](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017120227143.png)

### 传输示例

![image-20241017120557821](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017120557821.png)

![image-20241017120656830](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017120656830.png)

## DNS

### DNS的诞生

![image-20241017120843419](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017120843419.png)

DNS先在本地上找，没有的话去找对应的服务器 DNS封装在UDP上 数据库有的话会做响应

### 域名系统组成

![image-20241017121148435](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017121148435.png)![image-20241017121148584](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017121148584.png)

### 域名的表示方法

![image-20241017121253915](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017121253915.png)

### DNS查询方式

![image-20241017121421016](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017121421016.png)

## NTP

### 时间同步需求

![image-20241017134136542](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017134136542.png)

### NTP简介

![image-20241017134216630](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017134216630.png)

端口号**123**

### NTP网络结构

![image-20241017134432499](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017134432499.png)



DHCP回复所带内容的报文是DHCP Offer

根域名-> 顶级域名 -> 次顶级域名 -> 主机名
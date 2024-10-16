# ACL原理与配置

## ACL技术概述

### 技术背景：需要一个工具，实现流量过滤

![image-20241015151128085](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015151128085.png)

不希望研发部门访问财务部服务器，如果直接不设置对应路由的话，可能会影响到总裁和研发部之间的通信，那么就需要有一个过滤IP流量的工具，这个时候就需要用ACL进行实现了。

### ACL概述

![image-20241015151249863](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015151249863.png)

应用场景很广泛，ACL能把对应的数据挑拣出来，至于挑拣出来之后，怎么做都是可行的，具体看在对应的哪个位置。ACL只负责挑。

## ACL的基本概念及其工作原理

### ACL技术概述

#### ACL的组成

![image-20241015151709183](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015151709183.png)

ACL number 2000 列表的编号。

规则 rule 5 编号 动作 permit deny

可以根据很多方式挑地址

source 源IP地址 后面的是通配符掩码

可以通过IP地址以及通过它的通配符掩码来确定那一段范围是要找的数据

系统最后默认deny 有隐含规则 如果全都不适配选项，那么最后直接丢掉

![image-20241015152100252](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015152100252.png)

优先级为越小匹配的优先级越高，命令行步长可改。

### 通配符

![image-20241015153318582](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015153318582.png)

通配符0意味着指定10.1.1.1，0代指0.0.0.0 而255则代表最后一位可以随机分配，代表一个网段

![image-20241015153748304](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015153748304.png)

#### ACL的分类与标识

![image-20241015154106600](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015154106600.png)

#### 基本ACL和高级ACL

![image-20241015154155703](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015154155703.png)

高级ACL规则1允许 ip协议 源ip是 10.1.1.0 到 10.1.3.0 的协议通过

规则2 允许tcp协议 源ip 10.1.2.0 到 10.1.3.0 以及端口号为21的通过 ftp

其他默认deny

### ACL匹配机制

![image-20241015154532722](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015154532722.png)



如果不存在的话 就说明未做限制

### ACL匹配顺序及匹配结果

![image-20241015154735426](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015154735426.png)

ACL只负责挑数据，最终的应用场景看在哪里调用ACL

#### ACL的匹配位置

![image-20241015154928962](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015154928962.png)

#### 入站(Inbound)及出站(Outbound)

inbound指的接口收到数据，对于内网来说，比如流量从内网去访问互联网，对于接收接口来说，这就是inbound方向，对于链接互联网的方向，这个流量就应该在outbound上做一个过滤。

![image-20241015155306701](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015155306701.png)

## ACL的基础配置及应用

### 基本ACL的基础配置命令

1.创建基本ACL

---

[Huawei] **acl** [**number**] *acl-number* [ **match-order config**]

---

使用编号(2000~2999)创建一个数字型的基本ACL，并进入基本ACL视图。

---

[Huawei]**acl name** *acl-name*{**basic**|*acl-number*} [**match-order config**]

---

使用名称创建一个命名性的基本ACL，并进入基本ACL视图

2.配置基本ACL的规则

---

[Huawei-acl-basic-2000]**rule** [ *rule-id* ] {**deny|permit** } [**source** { *source-address source-wildcard*(通配符) | **any**} | {**time-range** *time-name*]

---

![image-20241015173334929](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241015173334929.png)

### 高级ACL

1.创建高级ACL

---

[Huawei] **acl** [**number**] *acl-number* [**match-order config**]

---

使用编号3000~3999创建一个数字型的高级ACL，并进入高级ACL视图

---

[Huawei]**acl name** *acl-name* {**advance** | *acl-number*} [**match-order** config]

使用名称创建一个命名形的高级ACL，并进入对应视图

2.配置高级ACL的基础配置命令

根据IP承载的协议类型不同，在设备上配置不同的高级ACL规则，对于不同的协议类型，有不同的参数组合。

- 当参数protocol为IP时，高级ACL的命令格式为

---

**rule** [*rule-id*] {**deny**|**permit**} **ip** [**destination** { *destination-address destination-wildcard*|**any**}|**source**{*source-address source-wildcard*|**any**} | **time-range** *time-name* | [**dscp** *dscp* | [**tos** *tos* | **precedence** *precendence*]]]

---

在高级ACL视图下，通过此命令来配置ACL的规则。

- 当参数protocol为TCP时，高级ACL的命令格式为

---

![image-20241016193137345](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241016193137345.png)

---




# WLAN概述

## WLAN概述

### 什么是WLAN

Wireless LAN，通过无线技术构建的无线局域网络。WLAN广义上是指以无线电波、激光、红外线等无线信号来有线局域网中的部分或全部传输介质所构成的网络(包括BT和NFC)

![image-20241017142033822](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017142033822.png)

### IEEE 802.11、WLAN和Wi-Fi

![image-20241017142638047](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017142638047.png)

WLAN包括Wifi 

WiFi属于共享介质  同一时间只能有一个人进行传输 CSMA/CA 冲突检测协议

### Wi-Fi在办公场景的发展趋势

BYOD:Bring Your Own Device

![image-20241017142938380](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017142938380.png)

## WLAN的基本概念

### WLAN设备介绍

家用的路由器(胖AP Fat-AP)集成度比较高， AP -> Access Point

企业用的AP一般都是瘦AP，只能完成无线方面的动作，这个时候就需要与另一台设备进行配合了，也就是AC(Access Controller)无线控制器来完成，AP只负责发送无线的信号，而由AC来负责管理层面的东西

PoE交换机不是一个必需品，但是也快成为了必需品。为什么需要呢，AP是有两个上行接口的，除此之外肯定也是需要进行供电的，毕竟不能用爱发电，但是企业中的AP一般都布置在天花板上面，而在天花板上面又不可能专门引一个插座，那怎么办呢，只能通过网线来给AP供电，毕竟网线里面的导线也是铜，铜也可以导电的。而这个导电的协议就是PoE(Power over Ethernet)协议，通过以太网供电，功率大概30W。现实生活当中的组网

![image-20241017144717964](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017144717964.png)

### 基本的WLAN组网架构

![image-20241017144824207](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017144824207.png)

胖AP基本上就是把接入层交换机换成了AP，然后通过以太网传输到上一层。

瘦AP连接在接入交换机上，通过传统的有线网络和AC进行一个相互通信，相互通讯的机制是CAPWAP，AC和AP通过有线侧进行连通，称为有线侧组网，往下AP对无线终端的叫做无线侧组网

### 敏捷分布式AP架构(用于宿舍）

走廊里有一个中心AP，每件宿舍都有一个敏分AP。起到一种类似信号放大器的用处

![image-20241017145232822](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017145232822.png)

酒店面板AP

### 有线侧组网概念：CAPWAP协议

![image-20241017145414296](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017145414296.png)

状态维护：APAC定期发送报文，感知到AC存在的话才会一直工作，感知不到的话就会下线，会自动重启

### 有线侧组网概念：AP-AC组网方式

组网方式是灵活多变的，不一定非要采用什么样的组网方式，会把常见的组网方式进行以下划分：二层和三层组网

APAC再在同一个网段  

![image-20241017145649361](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017145649361.png)

### 有线侧组网概念：AC连接方式

直连式组网和旁挂式组网

AP在往外部发的时候会经过AC，那么就是直连式组网，不经过就是旁挂式组网

![image-20241017145909261](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017145909261.png)

### 无线侧组网概念：无线通信系统

信源不能直接通过无线电波进行发送，需要进行编码调制，调制成无线信号才能通过空口(无线的天线)进行发送，怎么发？通过一些特定的频段进行发送，不同的频率也就有不同的信道。无线在传输的时候是有两个固定范围的频率2.4G和5G 后面还有具体范围。

无线电磁波对于信道的划分是

范围有标准 一般都是20 40 80 160 把20Mhz的频率绑在一起，同时进行一个信号的传输，传输频率越多，速率越快。

![image-20241017150629001](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017150629001.png)

### 无线侧组网概念：无线电磁波

![image-20241017152525391](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017152525391.png)

ac ax a n 都支持5G a的高频没啥用

### 无线侧组网概念：无线信道

![image-20241017152848872](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017152848872.png)

2.4GHz为了不产生干扰，一般通常只使用部分信道，例如 1 6 11、2 7 12等 国内一般不使用14

5Ghz支持信道捆绑，把2个80绑起来当160用，且在规划的时候信道就是没有任何重叠的。干扰出现的概率小。

### 无线侧组网概念：BSS/SSID/BSSID

![image-20241017153123885](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017153123885.png)

BSS集：只要手机能搜到无线信号，那么就在一个BSS集里

BSSID：虽然两个WLAN名称可能是一样的，但是要通过不同设备的MAC地址加BSSID来区分不同的WLAN

SSID:无线网络的名称

### 无线侧组网概念：VAP

![image-20241017153426481](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017153426481.png)

这个用途是用来解决例如外部的人Guest想要访问WiFi，和内部的人想要访问WiFi，利用VAP技术来将一个WiFi分成两个WiFi，分别提供不同的SSID和BSSID

### 无线侧组网概念：ESS

![image-20241017153631885](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017153631885.png)

扩展使用

在现实生活中，可能不管这些AP在哪里放着，但是它的这些SSID都是相同的，这样就组成了ESS，但BSSID也是不一样的。

## WLAN的工作原理

### WLAN工作流程概述

![image-20241017161624338](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017161624338.png)

> • AC+FIT AP组网架构中，是通过AC对AP进行统一的管理，因此所有的配置都是在AC上进行的。

### 步骤一：AP上线

![image-20241017161855013](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017161855013.png)

#### AP获取IP地址

方式：

- 静态：登录到AP上手动配置
- DHCP：通过DHCP Server获取，像Server请求

典型方案：

- 部署专门的DHCP Server
- 使用AC的DHCP服务为AP分配
- 使用网络中的设备，例如核心交换机为AP分配

DHCP方式

![image-20241017163116365](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017163116365.png)

#### CAPWAP隧道建立

![image-20241017163307035](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017163307035.png)

>• AP发现AC有两种方式： 
>
>​	▫ 静态方式：AP上预先配置AC的静态IP地址列表。 
>
>​	▫ 动态方式：DHCP方式、DNS方式和广播方式。 
>
>• AP与AC关联，完成CAPWAP隧道建立。包括数据隧道和控制隧道： 
>
>​	▫ 数据隧道：AP接收的业务数据报文经过CAPWAP数据隧道集中到AC上转发。 
>
>​	▫ 控制隧道：通过CAPWAP控制隧道实现AP与AC之间的管理报文的交互。 
>
>• CAPWAP隧道可以实现： 
>
>​	▫ AP与AC间的状态维护； 
>
>​	▫ AC对AP进行管理和业务配置下发； 
>
>​	▫ 业务数据经过CAPWAP隧道集中到AC上转发。 
>
>• AP发现AC阶段： 
>
>​	▫ 静态方式：AP上预先配置了AC的静态IP地址列表。AP上线时，AP分别发送 Discovery Request单播报文到所有预配置列表对应IP地址的AC。然后AP通过 接收到AC返回的Discovery Response报文，选择一个AC开始建立CAPWAP隧道。 
>
>​	▫ 动态方式：分为DHCP方式、DNS方式和广播方式，其中本章主要介绍DHCP 方式和广播方式。

#### Step1:AP动态发现AC

![image-20241017170545458](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017170545458.png)

> • DHCP方式： 
>
> ​	▫ 通过DHCP的四步交互过程，获取AC的IP地址： 
>
> ​		▪ 在没有预配置AC的IP列表时，则启动AP动态AC发现机制。通过DHCP获取IP地址，并通过DHCP协议中的Option返回AC地址列表（在DHCP服务器上配置 DHCP响应报文中携带Option 43，且Option 43携带AC的IP地址列表）。 
>
> ​		▪ 首先是AP发送DHCP Discover广播报文，请求DHCP Server响应，在DHCP服务器侦听到DHCP Discover报文后，它会从没有租约的地址范围中，选择最前面的闲置IP，连同其他TCP/IP设定，响应AP一个DHCP Offer报文，该报文中会包 含一个租约期限的信息。 
>
> ​		▪ 由于DHCP Offer报文既可以是单播报文，也可以是广播报文，当AP端收到多台DHCP Server的响应时，只会挑选其中一个Offer(通常是最先抵达的那个)，然后向网络中发送一个DHCP Request广播报文，告诉所有的Offer，并重新发送 DHCP，将指定接收哪一台服务器提供的IP地址。 
>
> ​		▪ 当DHCP Server接收到AP的Request报文之后，会向AP发送一个DHCP Ack响应， 该报文中携带的信息包括了AP的IP地址，租约期限，网关信息，以及DNS Server IP等，以此确定租约的正式生效，就此完成DHCP的四步交互工作。

#### Step2:建立CAPWAP隧道

![image-20241017171133229](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017171133229.png)

> • AP与AC关联，完成CAPWAP隧道建立。包括数据隧 道和控制隧道： 
>
> ​	▫ 数据隧道：AP接收的业务数据报文经过CAPWAP数据隧道 集中到AC上转发。同时还可以选择对数据隧道进行数据传输层安全DTLS（Datagram Transport Layer Security）加密，使能DTLS加密功能后，CAPWAP数据报文都会经过 DTLS加解密。 
>
> ​	▫ 控制隧道：通过CAPWAP控制隧道实现AP与AC之间的管理 报文的交互。同时还可以选择对控制隧道进行数据传输层 安全DTLS加密，使能DTLS加密功能后，CAPWAP控制报 文都会经过DTLS加解密。

#### Step3:AP接入控制

![image-20241017171156453](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017171156453.png)

>• 在收到AP发送的Join Request报文之后，AC会进行AP合法性的认证，认证通过则添加相应 的AP设备。 
>
>• AC上支持三种对AP的认证方式： 
>
>▫ MAC认证 
>
>▫ 序列号（SN）认证 
>
>▫ 不认证 
>
>• AC上添加AP的方式有三种： 
>
>​	▫ 离线导入AP：预先配置AP的MAC地址和SN，当AP与AC连接时，如果AC发现AP和预先增加的AP的MAC地址和SN匹配，则AC开始与AP建立连接。 
>
>​	▫ 自动发现AP：当配置AP的认证模式为不认证或配置AP的认证模式为MAC或SN认证且 将AP加入AP白名单中，则当AP与AC连接时，AP将被AC自动发现并正常上线。 
>
>​	▫ 手工确认未认证列表中的AP：当配置AP的认证模式为MAC或SN认证，但AP没有离线 导入且不在已设置的AP白名单中，则该AP会被记录到未授权的AP列表中。需要用户手工确认后，此AP才能正常上线。

#### Step4:AP的版本升级

![image-20241017171413105](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017171413105.png)

> • 在AC上给AP升级方式： 
>
> ​	▫ 自动升级：主要用于AP还未在AC中上线的场景。通常先配置好AP上线时的自动升级参数，然后再配置AP接入。AP在之后的上线过程中会自动完成升级。如果AP已经上线，配置完自动升级参数后，任意方式触发AP重启，AP也会进行自动升级。但相比于自动升级，使用在线升级方式升级能够减少业务中断的时间。 
>
> ​		▪ AC模式：AP升级时从AC上下载升级版本，适用于AP**数量较少**时的场景。 
>
> ​		▪ FTP模式：AP升级时从FTP服务器上下载升级版本，适用于**网络安全性要求不是很高**的文件传输场景中，采用**明文**传输数据，存在安全隐患。 
>
> ​		▪ SFTP模式：AP升级时从SFTP服务器上下载升级版本，适用于**网络安全性要求高**的场景，对传输数据进行了严格加密和完整性保护。 
>
> ​	▫ 在线升级：主要用于AP已经在AC中上线并已承载了WLAN业务的场景。 
>
> ​	▫ 定时升级：主要用于AP已经在AC中上线并已承载了WLAN业务的场景。通常指定在**网络访问量少**的时间段升级。

#### Step5：CAPWAP隧道维持

![image-20241017171807268](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017171807268.png)

> • 数据隧道维持： 
>
> ​	▫ AP与AC之间交互Keepalive (**UDP端口号为5247**)报文来检测数据隧道的连通状态。 
>
> • 控制隧道维持： 
>
> ​	▫ AP与AC交互Echo (**UDP端口号为5246**)报文来检测控制隧道的连通状态。

#### 为确保AP能够上线，AC需预先配置如下内容

![image-20241017172942735](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017172942735.png)

> • 域管理模板： 
>
> ​	▫ 域管理模板提供对AP的国家码、调优信道集合和调优带宽等的配置。 
>
> ​	▫ 国家码用来标识AP射频所在的国家，不同国家码规定了不同的AP射频特性，包括AP 的发送功率、支持的信道等。配置国家码是为了使AP的射频特性符合不同国家或区域 的法律法规要求。 
>
> • 配置AC的源接口或源地址： 
>
> ​	▫ 每台AC都必须唯一指定一个IP地址、VLANIF接口或者Loopback接口，该AC设备下挂 接的AP学习到此IP地址或者此接口下配置的IP地址，用于AC和AP间的通信。此IP地址 或者接口称为源地址或源接口。 
>
> ​	▫ 只有为每台AC指定唯一一个源接口或源地址，AP才能与AC建立CAPWAP隧道。 
>
> ​	▫ 设备支持使用VLANIF接口或Loopback接口作为源接口，支持使用VLANIF接口或 Loopback接口下的IP地址作为源地址。 
>
> • 添加AP设备：即配置AP认证模式，AP上线。 
>
> ​	▫ 添加AP有三种方式：离线导入AP、自动发现AP以及手工确认未认证列表中的AP。

### 步骤2：WLAN业务配置下发

![image-20241017173313719](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017173313719.png)

• AP上线后，会主动向AC发送Configuration Status Request报文，该信息中包含了现有AP 的配置，为了做AP的现有配置和AC设定配置的匹配检查。当AP的当前配置与AC要求不符合时，AC会通过Configuration Status Response通知AP。 

• 说明：AP上线后，首先会主动向AC获取当前配置，而后统一由AC对AP进行集中管理和业 务配置下发。

### 配置模板

![image-20241017173402340](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017173402340.png)

> • WLAN网络中存在着大量的AP，为了**简化AP的配置操作步骤**，可以将AP加入到AP**组**中，在 AP组中统一对AP进行同样的配置。但是每个AP也有着不同于其它AP的参数配置，不便于 通过AP组来进行统一配置，这类个性化的参数可以直接在每个AP下配置。每个AP在上线时 都会加入并且只能加入到一个AP组中。当AP从AC上获取到AP组和AP个性化的配置后，会 优先使用AP下的配置。 
>
> • AP组和AP下都能够引用如下模板：域管理模板、AP系统模板、射频模板、VAP模板，部 分模板例还能继续引用其它模板。 
>
> ​	▫ 域管理模板： 
>
> ​		▪ 国家码用来标识AP射频所在的国家，不同国家码规定了不同的AP射频特性，包括AP的发送功率、支持的信道等。配置国家码是为了使AP的射频特性符合不同国家或区域的法律法规要求。 
>
> ​		▪ 通过配置调优信道集合，可以在配置射频调优功能时指定AP信道动态调整的范 围，同时避开雷达信道和终端不支持信道。 
>
> ​	▫ 射频模板： 
>
> ​	▪ 根据实际的网络环境对射频的各项参数进行调整和优化，使AP具备满足实际需求的射频能力，提高WLAN网络的信号质量。射频模板中各项参数下发到AP后，只有AP支持的参数才会在AP上生效。 
>
> ​	▪ 可配置的参数包括：射频的类型、射频的速率、射频的无线报文组播发送速率、 AP发送Beacon帧的周期等。

### VAP模板

![image-20241017173857863](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241017173857863.png)

> • SSID模板：主要用于配置WLAN网络的SSID名称，还可以配置其他功能，主要包括如下功 能： 
>
> ​	▫ 隐藏SSID功能：用户在创建无线网络时，为了保护无线网络的安全，可以对无线网络 名称进行隐藏设置。这样，只有知道网络名称的无线用户才能连接到这个无线网络中。 
>
> ​	▫ 单个VAP下能够关联成功的最大用户数：单个VAP下接入的用户数越多，每个用户能 够使用的平均网络资源就越少，为了保证用户的上网体验，可以根据实际的网络状况配置合理的最大用户接入数。 
>
> ​	▫ 用户数达到最大时自动隐藏SSID的功能：使能用户数达到最大时自动隐藏SSID的功能 后，当WLAN网络下接入的用户数达到最大时，SSID会被隐藏，新用户将无法搜索到 SSID。 
>
> • 安全模板：配置WLAN安全策略，可以对无线终端进行身份验证，对用户的报文进行加密， 保护WLAN网络和用户的安全。 
>
> ​	▫ WLAN安全策略支持开放认证、WEP、WPA/WPA2-PSK、WPA/WPA2-802.1X等，在 安全模板中选择其中一种进行配置。

### 步骤3：STA接入

STA接入过程分为六个阶段：扫描阶段、链路认证阶段、关联阶 段、接入认证阶段、DHCP、用户认证。

#### 扫描阶段

![image-20241018162142386](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018162142386.png)

> • 携带有指定SSID的主动扫描方式：客户端发送携带有指定SSID的Probe Request：STA依次在每个信道发出Probe Request帧，寻找与STA有相同SSID的AP，只有能够提供指定SSID无线服务的AP接收到该探测请求后才回复探查响应。  -> 查找固定名字的WiFi名称
>
> • 携带空SSID的主动扫描方式：客户端发送广播Probe Request，客户端会定期地在其支持的 信道列表中，发送Probe Request帧扫描无线网络。当AP收到Probe Request帧后，会回应 Probe Response帧通告可以提供的无线网络信息。  -> 扫描
>
> • 主动扫描： 
>
> ​	▫ 携带有指定SSID的主动扫描方式：适用于STA通过主动扫描接入指定的无线网络。 
>
> ​	▫ 携带空SSID的主动扫描方式：适用于STA通过主动扫描可以获知是否存在可使用的无线服务。 
>
> • 被动扫描： 
>
> ​	▫ STA也支持被动扫描搜索无线网络。 
>
> ​	▫ 被动扫描是指客户端通过侦听AP定期发送的Beacon帧（信标帧，包含：SSID、支持 速率等信息）发现周围的无线网络，缺省状态下AP发送Beacon帧的周期为100TUs （1TU=1024us）。

#### 无线接入安全协议

![image-20241018162414078](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018162414078.png)

> • WLAN技术是以无线射频信号作为业务数据的传输介质，这种开放的信道使攻击者很容易对无线信道中传输的业务数据进行窃听和篡改。因此，安全性成为阻碍WLAN技术发展的最重要因素。 
>
> • WLAN安全提供了WEP、WPA、WPA2等安全策略机制。每种安全策略体现了一整套安全机制，包括无线链路建立时的链路认证方式，无线用户上线时的用户接入认证方式和无线用户传输数据业务时的数据加密方式。 
>
> • WEP（Wired Equivalent Privacy） 
>
> ​	▫ 有线等效加密WEP协议是由802.11标准定义的，用来保护无线局域网中的授权用户所传输的数据的安全性，防止这些数据被窃听。WEP的核心是**采用RC4算法**，加密**密钥长度**有**64位、128位和152位**，其中有24bit的IV（初始向量）是由系统产生的，所以WLAN服务端和WLAN客户端上**配置**的密钥长度是**40位、104位或128位**。WEP加密采用**静态的密钥**，接入**同一SSID**下的所有STA使用**相同的密钥**访问无线网络。 
>
> • WPA/WPA2 (Wi-Fi Protected Access) 
>
> ​	▫ 由于WEP共享密钥认证采用的是基于RC4对称流的加密算法，需要预先配置相同的静态密钥，无论从加密机制还是从加密算法本身，都很容易受到安全威胁。为了解决这个问题，在802.11i标准没有正式推出安全性更高的安全策略之前，Wi-Fi联盟推出了针对WEP改良的WPA。**WPA的核心加密算法还是采用RC4**，在WEP基础上提出了临时密钥完整性协议TKIP（Temporal Key Integrity Protocol）加密算法，采用了802.1X的身份验证框架，支持EAP-PEAP、EAP-TLS等认证方式。随后802.11i安全标准组织又推出WPA2，区别于WPA，WPA2采用安全性更高的区块密码锁链-信息真实性检查码协议CCMP（Counter Mode with CBC-MAC Protocol）加密算法。  
>
> ​	▫ 为了实现更好的兼容性，在目前的实现中,**WPA和WPA2**都可以使用**802.1X的接入认证、TKIP或CCMP**的加密算法，他们之间的不同主要表现在协议报文格式上，在安全性上几乎没有差别。 
>
> ​	▫ 综上所述，WPA/WPA2安全策略涉及了链路认证阶段、接入认证阶段、密钥协商和数据加密阶段。

#### 链路认证

![image-20241018164012085](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018164012085.png)

> • WLAN需要保障用户接入安全，即保障用户接入无线网络的合法性和安全性，STA接入WLAN网络前需要进行终端身份验证，即链路认证。链路认证通常被认为是终端连接AP并访问WLAN的起点。 
>
> • 共享密钥认证： 
>
> ​	▫ STA和AP预先配置相同的共享密钥，AP在链路认证过程验证两边的密钥配置是否相同。 如果一致，则认证成功；否则，认证失败。 
>
> ​	▫ 认证过程： 
>
>   		1. STA向AP发送认证请求（Authentication Request）。 
>   		2. AP随即生成一个“挑战短语（Challenge）”发给STA。 
>   		3. STA使用预先设置好的密钥加密“挑战短语”（EncryptedChallenge）并发给 AP。 
>   		4. AP接收到经过加密的“挑战短语”，用预先设置好的密钥解密该消息，然后将 解密后的“挑战短语”与之前发送给STA的进行比较。如果相同，认证成功； 否则，认证失败。

#### 关联

![image-20241018164235328](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018164235328.png)

> • 瘦接入点（FIT AP）架构中关联阶段处理过程： 
>
>  	1. STA向AP发送Association Request请求，请求帧中会携带STA自身的各种参数以及根据服务配置选择的各种参数（主要包括支持的速率、支持的信道、支持的QoS的能力等）。 
>  	2. AP收到Association Request请求帧后将其进行CAPWAP封装，并上报AC。 
>  	3. AC收到关联请求后判断是否需要进行用户的接入认证，并回应Association Response。 
>  	4. AP收到Association Response后将其进行CAPWAP解封装，并发给STA。

#### 接入认证

![image-20241018164418533](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018164418533.png)

> • 数据加密： 
>
> ​	▫ 除了用户接入认证外，对数据报文还需要使用加密的方式来保证数据安全，也是在接入认证阶段完成的。数据报文经过加密后，只有持有密钥的特定设备才可以对收到的报文进行解密，其他设备即使收到了报文，也因没有对应的密钥，无法对数据报文进行解密。

#### STA地址分配

![image-20241018164528815](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018164528815.png)

汇聚层能尽量的保证IP不重复，范围尽可能的大，便于配置

#### 用户认证

![image-20241018164610349](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018164610349.png)

> • 随着企业网络的应用和发展，病毒、木马、间谍软件、网络攻击等各种信息安全威胁也在不断增加。在传统的企业网络建设思路中，一般认为企业内网是安全的，安全威胁主要来自外界。但是研究证明，80%的网络安全漏洞都存在于网络内部。它们对网络的破坏程度和范围持续扩大，经常引起系统崩溃、网络瘫痪。另外，内部员工在浏览某些网站时，一些间谍软件、木马程序等恶意软件也会不知不觉地被下载到电脑中，并且在企业内网传播， 产生严重的安全隐患。 
>
> • 因此，随着安全挑战的不断升级，仅通过传统的安全措施已经远远不够。安全模型需要由被动模式向主动模式转变。从根源（终端）彻底解决网络安全问题，提高整个企业的信息安全水平。

### Step4 WLAN业务数据转发

#### 数据转发方式

![image-20241018164730078](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018164730078.png)

> • 隧道转发方式是指用户的数据报文到达AP后，需要经过CAPWAP数据隧道封装后发送给AC， 然后由AC再转发到上层网络。 
>
> • 直接转发方式是指用户的数据报文到达AP后，不经过CAPWAP的隧道封装而直接转发到上 层网络。 
>
> 
>
> • 隧道转发方式： 
>
> ​	▫ 优点：AC集中转发数据报文，安全性好，方便集中管理和控制。 
>
> ​	▫ 缺点：业务数据必须经过AC转发，报文转发效率比直接转发方式低，**AC所受压力大**。 
>
> • 直接转发方式： 
>
> ​	▫ 优点：数据报文不需要经过AC转发，报文转发效率高，AC所受压力小。 
>
> ​	▫ 缺点：业务数据不便于**集中管理**和控制。

## WLAN的配置实现

### 配置AP上线

1.配置AC作为DHCP，配置Option 43字段

---

[AC-ip-pool-pool1]**option** code [**sub-option** *sub-code*] {**ascii** *ascii-string*| **hex** *hex-string* | **cipher** *cipher-string* | **ip-address** *ip-address*

---

配置DHCP服务器分配给DHCP客户端的自定义选项

2.创建域管理模板，并配置国家码

---

[AC]**wlan**

[AC-wlan-view]

---

​	进入WLAN视图

---

[AC-wlan-view]**regulatory-domain-profile name** *profile-name*

[AC-wlan-regulate-domain-profile-name]

---

​	创建管理域模板，并进入模板视图，若模板已经存在则直接进入模板视图

---

[AC-wlan-regulate-domain-profile-name]**country-code** *country-code*

---

​	配置设备的国家码标识

---

[AC-wlan-view]**ap-group name** *group-name*

[AC-wlan-ap-group-group-name]

---

创建AP组，并进入AP组视图，若AP组已存在则直接进入AP组视图

---

[AC-wlan-ap-group-group-name]**regulatory-domain-profile** *profile-name*

---

将指定的域管理模板引用到AP或AP组

3.配置源接口或源地址

---

[AC]**capwap source interface** { **loopbabck** *loopback-number* | **vlanif** *vlan-id* }

---

配置AC与AP建立CAPWAP隧道的源接口

---

[AC]**capwap source Ip-address** *ip-address*

---

配置AC的源IP地址



4.添加AP设备-离线导入AP

---

[AC-wlan-view]**ap auth-mode** {**mac-auth**|**sn-auth**}

---

配置AP认证模式为MAC地址认证，或SN认证，缺省为MAC地址认证

---

[AC-wlan-view]**ap-id** *ap-id* [[**type-id** *type-id*|**ap-type** *ap-type*] { **ap-mac** *ap-mac* | **ap-sn** *ap-sn* | **ap-mac** *ap-mac* **ap-sn** *ap-sn*}]

[AC-wlan-ap-ap-id]**ap-name** *ap-name*

---

离线增加AP设备或进入AP视图，并配置单个AP的名称

---

[AC-wlan-view]**ap-id** *0*

[AC-wlan-view]**ap-group** *ap-group*

---

配置AP所加入的组。

5.检查AP上线结果

---

[AC]**display ap **{ **all | ap-group** *ap-group*}

---

查看AP信息

> • 命令：option code [ sub-option sub-code ] { ascii ascii-string | hex hex-string | cipher cipher-string | ip-address ip-address 
>
> ​	▫ code：指定自定义选项Option的数值。整数形式，取值范围1～254，但1、3、6、15、 44、46、50、51、52、53、54、55、57、58、59、61、82、121、184不能配置。 
>
> ​	▫ sub-option sub-code：指定自定义的Option子选项的数值。整数形式，取值范围是 1～254。知名选项请参考RFC2132。 
>
> ​	▫ ascii | hex | cipher：指定自定义的选项码为ASCII字符串类型，或十六进制字符串类 型，或密文字符串类型。 
>
> ​	▫ ip-address ip-address：指定自定义的选项码为IP地址类型。 
>
> • 命令：regulatory-domain-profile name profile-name ▫ name profile-name：指定域管理模板的名称。字符串类型，不区分大小写，可输入 的字符串长度为1～35个字符。可见字符，不能包含“?”和空格，双引号不能出现在 字符串的首尾。 
>
> • 命令：country-code country-code 
>
> ​	▫ country-code：指定设备的国家码标识。字符串格式，枚举类型。 
>
> ​	▫ AC支持的国家码有很多，如： 
>
> ​		▫ CN 中国（缺省值） 	
>
> ​		▫ AU 澳大利亚 
>
> ​		▫ CA 加拿大 
>
> ​		▫ DE 德国 
>
> ​		▫ FR 法国 
>
> ​		▫ US 美国 
>
> ​		▫ ……
>
> • 命令：ap-group name group-name ▫ name group-name：指定AP组的名称。字符串类型，可输入的字符串长度为1～35 个字符。可见字符，不能包含“?”、“/”和空格，双引号不能出现在字符串的首尾
>
> • 命令：ap-id ap-id [ [ type-id type-id | ap-type ap-type ] { ap-mac ap-mac | ap-sn ap-sn | ap-mac ap-mac ap-sn ap-sn } ] 
>
> ​	▫ ap-id：AP设备索引。整数类型，取值范围：0～8191。 
>
> ​	▫ type-id type-id：AP设备类型索引。整数类型，取值范围：0～255。 
>
> ​	▫ ap-type ap-type：AP设备类型。字符串类型，取值范围为1～31个字符。 
>
> ​	▫ ap-mac ap-mac：AP的MAC地址。格式为H-H-H，其中H为4位的十六进制数。 
>
> ​	▫ ap-sn ap-sn：AP的序列号。字符串类型，取值范围为1～31个字符，只能包括字母和数字。

### 配置射频

1. 进入射频视图

---

[AC-wlan-view]**ap-id** *0*

[AC-wlan-ap-0]**radio** *radio-id*

[AC-wlan-radio-0]

---

2. 配置指定射频的工作带宽和信道

---

[AC-wlan-radio-0/0]**channel** { **20mhz** | **40mhz-minus** | **40mhz-plus** | **80mhz** | **160mhz** } channel

Warning:This action may cause service interruption.Continue?[Y/N]y

---

---

[AC-wlan-radio-0/0]**channel** **80+80mhz** *channel1 channel2* 

Warning:This action may cause service interruption.Continue?[Y/N]y

---

配置AP组中所有AP或单个AP指定射频的工作带宽和信道



3. 配置天线的增益

---

[AC-wlan-radio-0/0]**antenna-gain** *antenna-gain*

---

配置AP组中所有AP或单个AP指定射频的天线增益



4.配置射频的发射功率

---

[AC-wlan-radio-0/0]**eirp** *erip*

---

配置AP组中所有AP或单个AP指定射频的发射功率



5.配置射频覆盖距离参数

---

[AC-wlan-radio-0/0]**coverage distance** *distance*

---



6.配置射频工作的频段

---

[AC-wlan-radio-0/0]**frequency {2.4g|5g}**

---



7.创建射频模板

---

[AC-wlan-view]**radio-2g-profile name** *profile-name*

---

创建2G射频模板，并进入模板视图，若模板已存在则进入模板视图



8.引用射频模板

---

[AC-wlan-view]**ap-group name** *group-name*

[AC-wlan-ap-group-group-name]**radio-2g-profile** *profile-name* **radio** {*raio-id* | **all**}

---

在AP组中，将指定的2G射频模板引用到2G射频

> • 命令：radio radio-id 
>
> ​	▫ radio-id：射频ID。必须是已存在的射频ID。 
>
> • 命令： 
>
> ​	▫ channel { 20mhz | 40mhz-minus | 40mhz-plus | 80mhz | 160mhz } channel 
>
> ​	▫ channel 80+80mhz channel1 channel2 ▫ 20mhz：指定射频的工作带宽为20MHz。 	
>
> ​	▫ 40mhz-minus：指定射频的工作带宽为40MHz Minus。 
>
> ​	▫ 40mhz-plus：指定射频的工作带宽为40MHz Plus。 
>
> ​	▫ 80mhz：指定射频的工作带宽为80MHz。 
>
> ​	▫ 160mhz：指定射频的工作带宽为160MHz。 
>
> ​	▫ 80+80mhz：指定射频的工作带宽为80+80MHz。 
>
> ​	▫ channel/channel1/channel2：指定射频的工作信道，信道基于国家代码和射频模式 来进行选择。枚举值类型，取值范围根据国家代码和射频模式来进行选择。 
>
> • 命令：antenna-gain antenna-gain 
>
> ​	▫ antenna-gain：天线增益。整数类型，取值范围：0～30，单位：dB
>
> • 命令：eirp eirp 
>
> ​	▫ eirp：发射功率值。整数形式，取值范围是1～127，单位：dBm。 
>
> • 命令：coverage distance distance 
>
> ​	▫ distance：射频覆盖距离参数。每个射频覆盖距离参数对应一组slottime、 acktimeout和ctstimeout数值。根据AP间的实际距离配置射频覆盖距离参数后，AP 设备根据此参数值调整对应的slottime、acktimeout和ctstimeout数值。整数类型， 取值范围：1～400，单位为100m。 
>
> • 命令：frequency { 2.4g | 5g } 
>
> ​	▫ 缺省情况下，射频0工作在2.4GHz频段，射频2工作在5GHz频段。
>
> • 命令：radio-2g-profile name profile-name 
>
> ​	▫ name profile-name：指定2G射频模板的名称。字符串类型，不区分大小写，可输入 的字符串长度为1～35个字符。可见字符，不能包含“?”和空格，双引号不能出现在 字符串的首尾。 
>
> ​	▫ 缺省情况下，系统上存在名为default的2G射频模板。 
>
> • 命令：radio-2g-profile profile-name radio { radio-id | all } 
>
> ​	▫ profile-name：指定2G射频模板的名称。必须是已存在的2G射频模板名称。 
>
> ​	▫ radio radio-id：指定射频的ID。整数类型，取值范围：0和2。 
>
> ​	▫ radio all：指定所有的射频。

### 配置VAP

1.创建VAP模板

---

[AC-wlan-view]**vap-profile name** *profile-name*

[AC-wlan-vap-prof-profile-name]

---

创建VAP模板，并进入模板视图，若模板已存在则直接进入模板视图

2.配置数据转发方式

---

[AC-wlan-vap-prof-profile-name]**forward-node**{**direct-forward**|**tunnel**}

---

配置VAP模板下的数据转发方式，可以使直接转发或隧道转发

3.配置业务VLAN

---

[AC-wlan-vap-prof-profile-name]**service-vlan** {**vlan-id** *vlan-id* | **vlan-pool** *pool-name*}

---

配置VAP的业务VLAN

4.配置安全模板

---

[AC-wlan-view]**security-profile name** *profile-name*

[AC-wlan-sec-prof-profile-name]

---

创建安全模板或者进入安全模板视图。

缺省情况下，系统已经创建名称为**default**、**default-wds**和**default-mesh**的安全模板。

---

[AC-wlan-view]**vap-profile name** *profile-name*

[AC-wlan-vap-prof-profile-name]**security-profile** *profile-name*

---

在指定VAP模板中引用安全模板

5.配置SSID模板

---

[AC-wlan-view]**ssid-profile name** *profile-name*

[AC-wlan-ssid-prof-profile-name]

---

创建SSID模板，并进入模板视图，若模板已存在则进入模板视图

缺省情况下，系统上存在名为**default**的SSID模板。

---

[AC-wlan-ssid-prof-profile-name]**ssid** *ssid*

---

配置当前SSID模板中的服务组合识别码SSID(Service Set Identifier)

缺省情况下，SSID模板中的SSID为HUAWEI_WLAN

---

[AC-wlan-view]**vap-profile name** *profile-name*

[AC-wlan-vap-prof-profile-name]**ssid-profile** *profile-name*

---

在指定VAP模板中引用SSID模板



6.引用VAP模板

---

[AC-wlan-view]**ap-group name** *group-name*

[AC-wlan-ap-group-group-name]**vap-profile** *profile-name* **wlan** *wlan-id* **radio** {*radio-id* | **all**}[**service-vlan** {**vlan-id** *vlan-id* | **vlan-pool** *pool-name}]

---

在AP组中，将指定的VAP模板引用到射频



7.查看VAP信息

---

[AC]**display vap** { **ap-group** *ap-group-name* | {**ap-name** *ap-name* | **ap-id** *ap-id*} [**radio** *radio-id*]} [**ssid** *ssid*]

[AC]**display vap** {**all** | **ssid** *ssid*}

---

查看业务型VAP的相关信息



> • 命令：ssid ssid 
>
> ​	▫ ssid：指定SSID的名称。文本类型，区分大小写，可输入的字符串长度为1～32字符， 支持中文字符，也支持中英文字符混合，不支持制表符。 
>
> ​	▫ 如果想设置SSID首字符为空格，则输入的SSID内容应该以“"”开头以“"”结束，如" hello"，其中前后的“"”占用两个字符。如果想设置SSID首字符为“"”，则需要在“"” 前输入转义字符“\”，如\"hello，其中“\”占用一个字符。
>
> • 命令：display vap { ap-group ap-group-name | { ap-name ap-name | ap-id ap-id } [ radio radio-id ] } [ ssid ssid ] 
>
> ​	▫ ap-group ap-group-name：查看指定AP组下的所有业务型VAP的相关信息。必须是已存在的AP组名称。 
>
> ​	▫ ap-name ap-name：查看指定名称的AP的业务型VAP的相关信息。必须是已存在的 AP名称。 
>
> ​	▫ ap-id ap-id：查看指定ID的AP的业务型VAP的相关信息。必须是已存在的AP ID。 
>
> ​	▫ radio radio-id：查看指定射频的业务型VAP的相关信息。整数类型，取值范围：0～2。 
>
> ​	▫ ssid ssid：查看指定SSID的业务型VAP的相关信息。必须是已存在的SSID。 
>
> • 命令：display vap { all | ssid ssid } 
>
> ​	▫ all：查看所有业务型VAP的相关信息。

## 新一代WLAN解决方案

WiFi6

![image-20241018211440846](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018211440846.png)![image-20241018211503118](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018211503118.png)

![image-20241018211612461](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018211612461.png)

![image-20241018211704528](./../../../../../AppData/Roaming/Typora/typora-user-images/image-20241018211704528.png)


## 华为VRP系统概述
### 什么是VRP
![[Pasted image 20241103093943.png]]
### VRP的发展
![[Pasted image 20241103094024.png]]
### 文件系统
![[Pasted image 20241103100020.png]]
有效管理硬件 使用对方的功能
启动文件(系统软件) ： .cc
配置文件 : .cfg .zip .dat
补丁文件 : .pat 啪！patch
PAF文件：对功能特性做剪裁使用
### 存储设备
![[Pasted image 20241103100319.png]]
Flash：配置一般存放在flash 类似sd卡 补丁文件也可以存 常用 断电不消失
SD Card: 希望设备有更多保险 放在主控板 存一份到卡上 非易失性 可拔
SDRAM： 运行内存
NVRAM： 存储日志缓存文件 存储日志
### 设备初始化过程
![[Pasted image 20241103100800.png]]
BootROM软件类似BIOS
Basic In Out System
红字之后开始加载
### 设备管理(配置)
![[Pasted image 20241103101014.png]]
Web会更人性化一些
通过字符串进行管理 简单 快捷  先用Console口
### VRP用户界面
![[Pasted image 20241103101532.png]]
### VRP用户级别
![[Pasted image 20241103101718.png]]
0 等级低 查看配置
1 监控机 系统维护
2 配置级 部分配置
3 管理级 基本上所有命令都可以使用

分配好级别之后就可以登录了

### WEB网管方式登录
![[Pasted image 20241103101903.png]]
### 命令行方式 本地登录
![[Pasted image 20241103101937.png]]
确定好打开之后 使用putty登录
![[Pasted image 20241103101956.png]]
### 远程登录
![[Pasted image 20241103102031.png]]
Telnet和SSH需要配置端口号
### 命令行界面
![[Pasted image 20241103102103.png]]

## 命令行基础
### 命令行视图
![[Pasted image 20241103103410.png]]
![[Pasted image 20241103103451.png]]
### 编辑命令行
![[Pasted image 20241103103547.png]]
![[Pasted image 20241103103654.png]]
### 使用命令行在线帮助
![[Pasted image 20241103103732.png]]
### 解读命令行的错误信息
![[Pasted image 20241103103917.png]]
### undo命令行
![[Pasted image 20241103104009.png]]
### 使用命令行的快捷键
![[Pasted image 20241103104041.png]]
### 常见文件系统操作命令
用户视图~
![[Pasted image 20241103104148.png]]
![[Pasted image 20241103104214.png]]
![[Pasted image 20241103104229.png]]
![[Pasted image 20241103104320.png]]
![[Pasted image 20241103104447.png]]
cipher用来配置输入的密码在显示上为乱码
![[Pasted image 20241103104634.png]]
![[Pasted image 20241103104706.png]]
### VRP基本配置命令
![[Pasted image 20241103104734.png]]
![[Pasted image 20241103104827.png]]
![[Pasted image 20241103104846.png]]
![[Pasted image 20241103104922.png]]
## WLAN设备升级
### 为什么要升级
![[Pasted image 20241103110518.png]]
### AC升级
![[Pasted image 20241103110535.png]]
#### 升级前准备
![[Pasted image 20241103110606.png]]
#### 下载系统软件
![[Pasted image 20241103110640.png]]
#### 加载系统软件
![[Pasted image 20241103110703.png]]
#### 重启设备
![[Pasted image 20241103110718.png]]
### AP升级
由AC控制
![[Pasted image 20241103110804.png]]
#### 升级模式 AC-Mode
![[Pasted image 20241103110821.png]]
#### 查看AP上线状态
![[Pasted image 20241103110853.png]]
#### 升级状态
![[Pasted image 20241103110916.png]]
#### 上线状态
![[Pasted image 20241103110925.png]]
#### 重启AP
![[Pasted image 20241103111007.png]]

## 配置FAT AP
### AP-胖瘦一体
![[Pasted image 20241103111834.png]]
### AP模式切换步骤
- 环境准备
- 查看AP信息
- 开始切换
- 切换后检查
![[Pasted image 20241103112004.png]]
![[Pasted image 20241103112012.png]]
### FAT AP配置
![[Pasted image 20241103112041.png]]
![[Pasted image 20241103112048.png]]
![[Pasted image 20241103112131.png]]
### 案例：FAT AP二层组网
![[Pasted image 20241103112158.png]]
#### 配置网络互通
![[Pasted image 20241103112239.png]]
#### 配置WLAN业务参数
![[Pasted image 20241103112305.png]]
![[Pasted image 20241103112343.png]]

#### 查看STA连接信息
![[Pasted image 20241103112404.png]]

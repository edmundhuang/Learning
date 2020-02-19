# CentOS 8 安装及基本配置
最小化 CentOS 8
用户：root/centos8
用户：demo8/abcd1234

1. 网络设置
```
ifconfig
```
新安装好的centos8默认网卡是没有启动的，安装好后需要先配置网络。

在/etc/sysconfig/network-scripts目录下存放着网卡的配置文件，文件名称是ifcfg- 网卡名称。
```
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
> # 网卡配置文件按默认配置
TYPE=Ethernet  
PROXY_METHOD=none  
BROWSER_ONLY=no  
BOOTPROTO=dhcp  
DEFROUTE=yes  
IPV4_FAILURE_FATAL=no  
IPV6INIT=yes  
IPV6_AUTOCONF=yes  
IPV6_DEFROUTE=yes  
IPV6_FAILURE_FATAL=no  
IPV6_ADDR_GEN_MODE=stable-privacy  
NAME=ens33  
UUID=e4987998-a4ce-4cef-96f5-a3106a97f5bf  
DEVICE=ens33  
ONBOOT=no   

#如果使用dhcp分配ip的话，只需要将这里ONBOOT=no改为yes，然后重启网络服务就行  

重启网络服务
```bash
nmcli c reload
```
2. 安装 ifconfig, minimal install 不包含ifconfig
```
yum install net-tools
```

3. 安装DNF
Currently the DNF package comes from the EPEL repository, so if your Linux system is not already configured to use this repository, simply run the command below to set it up.
```
yum install epel-release -y
```
Now that EPEL is ready to use, simply install the dnf package as shown below.
```
yum install dnf -y
```

4. 更新系统  -- 貌似第三步不做也可以运行。
```
dnf update -y
```
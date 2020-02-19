# 安装 CentOS

1. [CentOS8 安装及配置](./centos8/init.md)




1. 下载 
URL: centos.org
http://centos.nethub.com.hk/8.1.1911/isos/x86_64/CentOS-8.1.1911-x86_64-dvd1.iso
Size: 7G DVD ISO

2. 安装
* Hyper-V 虚拟机必须选择第一代  

### 

1. 网络设置
```ifconfig```
新安装好的centos8默认网卡是没有启动的，安装好后需要先配置网络。

在/etc/sysconfig/network-scripts目录下存放着网卡的配置文件，文件名称是ifcfg- 网卡名称。
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
1.2. 安装 ifconfig, minimal install 不包含ifconfig
```
yum install net-tools
```

1.3. 安装DNF
Currently the DNF package comes from the EPEL repository, so if your Linux system is not already configured to use this repository, simply run the command below to set it up.
```
yum install epel-release -y
```
Now that EPEL is ready to use, simply install the dnf package as shown below.
```
yum install dnf -y
```

2. 更新系统
```
dnf update
```

3. 检查 SSH-Server 是否安装
```
yum list installed |grep openssh-server
```
> 模块依赖问题
> 问题1： conflicting requests
- nothing providees module(perl:5.26) needed by module perl-DBD-SQLite:1.58:......
问题2： conflicting requests
- nothing provides module(perl:5.26) needed by module perl-DBI:1.641:.....
openssh-server.x86_64   8.0pl-3.el8

```
rpm -qa |grep ssh-server
```

> openssh-server-8.0pl-3.el8.x86_64

测试SSH连接
Windows 10 内置 OpenSSH Client
```
ssh hcc@192.168.1.142
```

3. 安装 postfix
https://www.linuxtechi.com/install-configure-postfix-mailserver-centos-8/
Step 1) Update the system
Step 2)  Set Hostname and update /etc/hosts file
Before proceeding further, also ensure that no other MTAs such as Sendmail are existing as this will cause conflict with Postfix configuration. To remove Sendmail, for example, run the command:
```
dnf remove sendmail
```

```
dnf install postfix
```
下载大小1.5M, 安装大小5.4M.

Start and enable Postfix service after the installation.
```
sudo systemctl enable postfix && sudo systemctl start postfix
```

### Install GitLab
```
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```

Message
>The repository is setup! You can now install packages.

```
yum install gitlab-ce
```


4.  Add the Gitlab CE Repository
GitLab provides omnibus packages from a repository. These packages are compiled specifically for CentOS/RHEL.
Create a new repository file for GitLab:
```
sudo vi /etc/yum.repos.d/gitlab-ce.repo
```
Then add the following lines:
```
[gitlab-ce]
name=gitlab-ce
baseurl=https://packages.gitlab.com/gitlab/gitlab-ce/el/7/$basearch
repo_gpgcheck=1
gpgcheck=1
enabled=1
gpgkey=https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey
       https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey/gitlab-gitlab-ce-3D645A26AB9FBD22.pub.gpg
metadata_expire=300
```

5. Install Gitlab CE on CentOS / RHEL 8
```
sudo yum install -y gitlab-ce --nobest
```
6.  Configure GitLab CE
```
sudo vi /etc/gitlab/gitlab.rb
```

E.g, Set URL on which GitLab will be reachable:
> external_url 'http://gitlab.example.com'

Scroll through the configuration file and make changes accordingly. Once done, save the file and run Gitlab reconfiguration script.
```
sudo gitlab-ctl reconfigure
```


If you have an active firewall, allow http, https and ssh services.
``` bash
sudo firewall-cmd --permanent --add-service={ssh,http,https} --permanent
sudo firewall-cmd --reload
```

查看防火墙状态
```
firewall-cmd --state
```
#查看默认防火墙状态（关闭后显示notrunning，开启后显示running）

7. 需要先安装Ruby
```
dnf install ruby
```
否则下一步会出错。
8. 启动GitLab
```
sudo gitlab-ctl reconfigure
```
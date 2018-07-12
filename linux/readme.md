# Linux 常见问题

1. 如何查看系统版本  
```
cat /etc/*release

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.2 LTS"
NAME="Ubuntu"
VERSION="16.04.2 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.2 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
```

2、apt-get install wget 提示“unable to locate package wget”
更新 apt-get
``` bash
apt-get update  
```

3、 apt-get install wget 
```
apt-get install wget
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  ca-certificates libidn11 libssl1.0.0 openssl
The following NEW packages will be installed:
  ca-certificates libidn11 libssl1.0.0 openssl wget
0 upgraded, 5 newly installed, 0 to remove and 40 not upgraded.
Need to get 2089 kB of archives.
After this operation, 6027 kB of additional disk space will be used.
Do you want to continue? [Y/n]
```
加入 -y 可以静默安装


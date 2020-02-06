# Windows Subsystem for Linux 2

1. [Docker in WSL](./docker.md)

### 安装 XFCE 桌面及配置 XRDP 远程桌面
1. 
``` bash
sudo apt install xorg
```
大约需要485M 磁盘空间。

期间如果出现 404 Not Found，可用下列命令修复
```
apt-get update --fix-missing
```

2. 安装 xfce 桌面环境
``` bash
sudo apt install xfce4
```
大约需要 125MB 空间

3. 安装 xrdp 远程桌面
``` bash
sudo apt install xrdp
```
大约需要 3.3MB 空间

4. 设置 xRDP
``` bash
echo xfce4-session >~/.xsession
```

5. 修改配置文件 
``` bash
sudo vi /etc/xrdp/startw.sh
```

6. 查看 xrdp 状态
``` bash
/etc/inint.d/xrdp status
```

未运行，显示
> * xrdp-sesman is not running
* xrdp is not running

运行在，显示
> * xrdp-sesman is running
* xrdp is running

7. 启动/重启 xrdp
``` bash
sudo service xrdp restart
```




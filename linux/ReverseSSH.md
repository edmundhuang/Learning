# Reverse SSH

A: 中转服务器
ip: 172.26.196.79
demo8 /abcd1234
转发端口：88

B: 目标服务器
ip: 172.26.205.71
80 服务 - gitlab 网站

### 实验过程
1、目标服务器生成密钥
```
ssh-keygen -t rsa 
# -t type  rsa1(SSH1)/dsa(SSH2)/ecdsa(SSH2)/rsa(SSH2) 等类型
# -C comment 提供一个新的注释
# -b bits， 密钥长度，RSA，最小长度768bits,默认长度为2048bits, DSA密钥必须是1024bits
```

密钥默认保存在 /home/(username)/.ssh/id_rsa 文件中，
公钥文件名 id_rsa.pub

2. 推送公钥文件到中转服务器
```
ssh-copy-id demo8@172.26.196.79
```

3. SSH连接服务器测试
```
ssh demo8@172.26.196.79
```
成功的标志是不需要输入密码，直接连接。

4. 配置反向隧道
服务端
```
ssh -R 8080:172.26.205.71:80 demo8@172.26.196.79
```
```
ssh -NfR 8080:0.0.0.0:80 demo8@172.26.196.79
# -N: 只建立连接，不打开shell
# -f: 建立成功后在后台运行
# -R：指定端口映射（反向）
```

中转端

```
vi /etc/ssh/sshd_config
```
设置
> GatewayPorts yes

查看防火墙状态
```
firewall-cmd --state
```
关闭防火墙 - 测试临时措施
```
systemctl stop firewalld.service
```
禁止防火墙开机启动
```
systemctl disable firewalld.service
```

4. 添加服务到防火墙
复制http.xml
```
cp /usr/lib/firewalld/services/http.xml /etc/firewalld/services
```
改名
```
cd /etc/firewalld/services
mv http.xml forward-http.xml
```
改内容
```
vi forward-http.xml
```
><?xml version="1.0" encoding="utf-8"?>
<!-- http.xml -->
<service>
    <short>WWW (Forward-HTTP)</short>
    <description>HTTP is the protocol used to serve Web pages. If you plan to make your Web server publicly available, enable this option. This option is not required for viewing pages locally or developing Web pages.</description>
    <port protocol="tcp" port="8080"/>
</service>

添加 forward-http 到防火墙中， 并重启防火墙。
```
firewall-cmd --permanent --add-service=forward-http
firewall-cmd --reload 
```



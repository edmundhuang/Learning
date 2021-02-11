# frp 配置

1. 下载frp
frp_0.31.2_linux_amd64.tar.gz

2. Winscp 上传
/usr/local/frp

3. tar 解压缩
tar -zxvf frp_0.31.2_linux_amd64.tar.gz

4. 修改服务器端配置
```
[common]
bind_addr = 0.0.0.0. #此处填写你的公网ip，阿里云服务器都有的！
bind_port = 56023
dashboard_port = 56024
dashboard_user = frpAdmin
dashboard_pwd = Admin1234%
log_file = ./frps.log
log_level = error
log_max_days = 3
token = Qazwsx123$%^1
12max_pool_count = 50
tcp_mux = true
```

5. 运行 frps 服务
```
nohup ./frps -c ./frps.ini &
```

6. 修改客户端配置
```
[common]
server_addr = 202.175.81.201
server_port = 56023

# for authentication
token = 123456789101112

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 3389
remote_port = 56089
```
7. 运行 frpc 客户端
```
frpc -c frpc.ini
```

7. 让 frpc 运行在 Windows 服务
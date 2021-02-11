# Basic Command

1. 查看版本
``` 
cat /etc/.release 

cat /etc/os-release # CentOS 8
```
2. 重启SSH服务
```
service sshd restart
```

3. 创建用户
可以直接利用adduser创建新用户（adduser +用户名）这样在/home目录下会自动创建同名文件夹
```
adduser hcc
# 设置密码
passwd hcc  
```

4. 改文件名
在linux下重命名文件或目录，可以使用mv命令或rename命令，这里分享下二者的使用方法。  
mv命令既可以重命名，又可以移动文件或文件夹。  
例子：将目录A重命名为B  
mv A B  
例子：将/a目录移动到/b下，并重命名为c  
mv /a /b/c  
其实在文本模式中要重命名文件或目录，只需要使用mv命令就可以了，比如说要将一个名为abc的文件重命名为1234：  
mv abc 1234  
注意，如果当前目录下也有个1234的文件的话，这个文件是会将它覆盖的。  
下面介绍linux系统中另一个重命名命令 rename命令的用法。  

5. 查看端口占用情况 lsof /netsat
lsof -i:端口号

```
lsof -i:8000
```

>COMMAND   PID USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME  
nodejs  26993 root   10u  IPv4 37999514      0t0  TCP *:8000 (LISTEN)

更多 lsof 的命令如下：
```
lsof -i:8080：查看8080端口占用
lsof abc.txt：显示开启文件abc.txt的进程
lsof -c abc：显示abc进程现在打开的文件
lsof -c -p 1234：列出进程号为1234的进程所打开的文件
lsof -g gid：显示归属gid的进程情况
lsof +d /usr/local/：显示目录下被进程开启的文件
lsof +D /usr/local/：同上，但是会搜索目录下的目录，时间较长
lsof -d 4：显示使用fd为4的进程
lsof -i -U：显示所有打开的端口和UNIX domain文件
```

6. 查看内存、硬盘
```
free  # 内存
df -m # 以MB为单位显示磁盘使用量。
```
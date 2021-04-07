### 使用命令行导入大数据量SQL脚本
用SQL Server Management Studio导入大数据量SQL脚本时，很容易出现了out of memory异常，可用命令行导入
打开cmd执行命令：
```
#-S 服务器地址 -U 用户名 -P 密码  -d 数据库名称 -i 脚本文件路径 
sqlcmd -S localhost -U sa -P 1 -d yanan -i yanan.sql
#例：
sqlcmd -S 192.168.8.220 -U sa -P Evget123456789 -d MagnetsMes_sm0113 -i I:\sm\202001131033.sql
```
原文链接：https://blog.csdn.net/WZH577/article/details/103955693
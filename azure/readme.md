# Azure 

创建虚拟机需要6个基本资源 Resource
* Virtual network 虚拟网络
* Public IP address 公共IP分配
* Network interface 网络接口
* Network security group 网络安全组
* Virtual machine 虚拟机
* Disk 硬盘

### 注册免费账号
* 12 個月免費的熱門服務
* 25+ 個永遠免費的服務
* 在前 30 天有 $200 的點數可用

日期：2021-04-07
 edmund1973@msn.com
 visa: 4709 4280 0440 8703

 https://portal.azure.com/

 1. 创建B1- Linux, Net Core 3.1 LTS App Service
 #### 创建SQL 数据库
 1. 新建服务器
 服务器名称： macaupuda.database.windows.net
 管理员： edmundwong
 密码： Macau1d66d734

## 安装 Azure CLI
powershell 执行以下命令
```
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
```

* [Reference Link](./reference.md)

1. [还原数据库备份到本地SQL数据库实例](https://www.cnblogs.com/lwqlun/p/11017422.html)
sqlpackage.exe location:  
C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\150
Backup:
```
sqlpackage /Action:export /SourceConnectionString:"Data Source=(localdb)\mssqllocaldb;Initial Catalog=CloudpressBackup;Integrated Security=true;" /TargetFile:"d:\bak\xiwen.bacpac"
```


```
sqlpackage.exe /Action:Import /SourceFile:"d:\bak\xiwen-2021-10-25-18-28.bacpac" 
/TargetConnectionString:"Data Source=(localdb)\mssqllocaldb;Initial Catalog=CloudpressBackup;Integrated Security=true;"
```

### Copy qimingsi upload folder to blob container using SAS token.
 .\azcopy  copy upload\*.* "https://macaupuda.blob.core.windows.net/qimingsi?sp=racwdl&st=2021-10-11T10:06:59Z&se=2021-10-11T18:06:59Z&spr=https&sv=2020-08-04&sr=c&sig=AXnm%2BevXFs2z9KZpieGkKuKTHwBUCciV20AfOt7pXQ0%3D"

  .\azcopy  copy upload\*.* "https://macaupuda.blob.core.windows.net/qimingsi?sp=racwdl&st=2021-10-11T10:06:59Z&se=2021-10-11T18:06:59Z&spr=https&sv=2020-08-04&sr=c&sig=AXnm%2BevXFs2z9KZpieGkKuKTHwBUCciV20AfOt7pXQ0%3D"
INFO: Scanning...
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support

Job 93fffc46-f9cf-464d-63e0-f54835583078 has started
Log file is located at: C:\Users\hcc\.azcopy\93fffc46-f9cf-464d-63e0-f54835583078.log

99.6 %, 2115 Done, 0 Failed, 5 Pending, 0 Skipped, 2120 Total,


Job 93fffc46-f9cf-464d-63e0-f54835583078 summary
Elapsed Time (Minutes): 30.0943
Number of File Transfers: 2120
Number of Folder Property Transfers: 0
Total Number of Transfers: 2120
Number of Transfers Completed: 2120
Number of Transfers Failed: 0
Number of Transfers Skipped: 0
TotalBytesTransferred: 623700456
Final Job Status: Completed


### Issues
1. Free web app service will be idled after 20 minutes without visit.
2. 
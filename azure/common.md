### Blob 

### Azcopy 
1. Copy
```
azcopy copy "<local-folder-path>" "https://<storage-account-name>.<blob or dfs>.core.windows.net/<container-name>" --recursive=true
```

* 将 <local-folder-path> 占位符替换为包含文件（例如 C:\myFolder 或 /mnt/myFolder）的文件夹的路径。
* 将 <storage-account-name> 占位符替换为存储帐户的名称。
* 请将 <container-name> 占位符替换为所创建容器的名称。
* 若要将指定目录的内容以递归方式上传到 Blob 存储，请指定 --recursive 选项。 使用此选项运行 AzCopy 时，会同时上传所有子文件夹及其文件。

2. Sync
Use sas token
```
azcopy sync "./uploads" "https://pudadev.blob.core.windows.net/qimingsi?sp=racwdl&st=2022-03-15T04:11:37Z&se=2022-03-15T12:11:37Z&spr=https&sv=2020-08-04&sr=c&sig=NHSamO%2FHAkqpCXvGfiMB%2B9qNNQOpiNFJHKoK7%2F71r7A%3D"
```


### Reference
1. [使用 AzCopy 将本地数据迁移到云存储空间](https://docs.microsoft.com/zh-cn/azure/storage/common/storage-use-azcopy-migrate-on-premises-data?tabs=windows)
2. [AzCopy for Azure Storage](https://www.thomasmaurer.ch/2019/05/how-to-install-azcopy-for-azure-storage/)
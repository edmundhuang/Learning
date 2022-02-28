# Git 学习资源

## Git 常用命令
1. 添加远程仓库
``` bash
git remote add origin https://github.com/edmundhuang/Learning.git  
git push -u origin master
```

已有项目
Step 1: Switch to your repository's directory
```bash
cd /path/to/your/repo
```

Step 2: Connect your existing repository to Bitbucket
```bash
git remote add origin https://edmundhuang@bitbucket.org/edmundhuang/temple.git
git push -u origin master
```

2. 导出差异，应用到另外一个repo
生成patch 文件
```
git format-patch 70685bb3
```
console output as below  
> PS D:\P\Larc\Larc.CasinoAsset> git format-patch 70685bb3  
0001-try-master-detail-ui.patch

应用patch
```
git apply 0001-try-master-detail-ui.patch
```
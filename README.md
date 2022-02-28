# Learning
学习资源整理


### 删除 Visual Studio 占空间DLL
https://stackoverflow.com/questions/755382/i-want-to-delete-all-bin-and-obj-folders-to-force-all-projects-to-rebuild-everyt

git bash 下运行
```
find . -iname "bin" -o -iname "obj" | xargs rm -rf
find . -iname "packages" | xargs rm -rf
find . -iname "node_modules" | xargs rm -rf
```
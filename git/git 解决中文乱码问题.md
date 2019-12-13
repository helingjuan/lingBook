---
title: git 解决中文乱码问题
tags: 
notebook: git
---
# git 解决中文乱码问题
## 概述
在windows下用git，如果上传啊，提交备注啊，如果出现中文就乱码，就像这样
```
\345\255\246\344\271\240\350\256\260\345\275\225/
```
这样就很不方便了。所以我们要看到中文！
## 解决
在终端输入一个命令就好了:+1:(亲测有用！)
```
git config --global core.quotepath false
```
## 参考资料
- [git status 显示中文和解决中文乱码(CSDN-铁乐与猫)](https://blog.csdn.net/u012145252/article/details/81775362)


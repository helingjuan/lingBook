---
title: win10 环境下升级nodeJS
tags: nodeJS
notebook: 前端
---
# win10 环境下升级nodeJS
因为之前安装的版本低了，所以现在要升级nodeJS环境，我的环境是win10

百度了波，发现要手动安装emmmmm   
**注意！那个n模块的命令在windows环境是不支持的**
如果你真的要试的话，你就会和我看到一样的报错：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191126151559.png)
就是说这个n模块，是在非window环境下的安装的，你windows不能安装！

## 正确的升级途径
1. 去官网的[下载地址](https://nodejs.org/en/download/)下载最新的msi文件，
2. 然后去cmd里输入 `where node` 找到node的安装地址
3. 用最新的安装包覆盖旧的，即可！
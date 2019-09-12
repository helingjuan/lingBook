---
title: git 报错 Cannot update the ref 'ORIG_HEAD'.
tags: git
notebook: git
---
# git 报错 Cannot update the ref 'ORIG_HEAD'.
Cannot update the ref 'ORIG_HEAD'.

具体的报错信息：
```
error: Couldn't set ORIG_HEAD
fatal: Cannot update the ref 'ORIG_HEAD'.
```
解决方法：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190812164218.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190812164157.png)
找到这个文件夹下，git的隐藏文件夹，找到`ORIG_HEAD`这个文件，删掉！对没错！你没看错，就是删掉它。
然后再拉取一下`git pull`
就好了。



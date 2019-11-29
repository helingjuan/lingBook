---
title: select2 遇到的问题：样式错位等
tags: 插件
notebook: 前端
---
# select2 遇到的问题：样式错位等
总是有各种奇奇怪怪的问题，头疼。
### 1.样式错位
比如这样：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190918115114.png)
本来应就一个下拉框的，里面带了搜索的，结果搜索部分内容跑到外面来了。有毒。  
#### 解决：  
哇，睡了午觉，问题解决。我真是优秀！
**问题就是select2.min.css这个样式没有加载进来！加载进来就好啦。**
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190918141839.png)


### 2.光标高亮错位了，错的乱七八糟
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/select2-bug.gif)
这。。。。我真的是不知道为什么了。生气！

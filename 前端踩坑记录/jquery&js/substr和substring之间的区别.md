---
title: substr和substring之间的区别
tags: 
notebook: 
---
# substr和substring之间的区别
——这两个都是截取字符串的。
都可以输入1个或2个参数。
### 1个参数：substr(index) && substring(index)
当**参数是1个时，substr和substring的结果是一样的**：都是截取字符串当前下标以后直到字符串最后的字符串片段。   
举例：   
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190820164521.png)   
### 2个参数：substr(a, b) && substring(a, b)
当**参数是2个时，就开始有区别**了
- substr(a, b) 是截取坐标a之后b个字符的字符串
- substring(a, b) 是截取坐标a到坐标b之间的字符串
举例：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190820164530.png)



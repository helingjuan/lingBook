---
title: 用Chrome模拟其它的浏览器，比如微信浏览器
tags: 
notebook: 工具
---
# 用Chrome模拟其它的浏览器，比如微信浏览器
因为有时候需要验证在其它浏览器的情况，又不可能把所有浏览器都安装了，比如微信内置的浏览器，就测试不了。所以就需要这个工具了！就是谷歌控制台自带的，很方便。  
路径是：  
去More Tools -> Network conditions ，打开这个工具，就可以进行模拟测试了。  
具体如下截图
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191129100153.png)

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191129100258.png)

如果你要模拟的是这里所没有的，那就可以进行自定义，把你要模拟的那个浏览器的userAgent 输入，即可模拟（可在你要模拟的那个浏览器的控制台中，输入`navigator.userAgent`获取那个浏览器的userAgent），比如微信浏览器   

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191129101043.png)

## 参考资料
- [JS如何判断浏览器类型，如何模拟浏览器类型（模拟微信浏览器）(博客园——南歌子)](https://www.cnblogs.com/nangezi/p/9342619.html)


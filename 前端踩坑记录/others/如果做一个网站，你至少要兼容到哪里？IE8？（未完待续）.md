---
title: 网站兼容性要怎么考虑？
tags: 前端
notebook: 前端
---
# 如果做一个网站，你至少要兼容到哪里？IE8？ios6？
在做网站的时候，一般都要先考虑这个问题，再开始技术选型。根据网站定位，就能知道会打开这个网站的目标客户是什么情况的，就能大致知道要兼容到几。

emmmm，之所以会开始思考这个，当然是我又双叒在写官网啦。虽然官网一般都比较简单，但是因为之前有了前车之鉴，这次就更细致了。
先看几种百度的数据，来源：[百度统计](https://tongji.baidu.com/data/hour)（该网站用了flash，建议用火狐打开）
![image](https://github.com/heihuahe/myGallery/raw/master/noteImage/static-img.png)
![image](https://github.com/heihuahe/myGallery/raw/master/noteImage/static-img-2.png)
![image](https://github.com/heihuahe/myGallery/blob/master/noteImage/static-img-3.png)
### 有哪些网站定位
网站定位有这么几种：系统，房地产，时尚，电子等。
我的就是系统啦。系统网站其实结构很简单，主要是介绍自己的系统、客户、解决方案以及所属公司的信息等等。

### 目标客户
说到系统网站，不得不提政府系统了，政府系统，顾名思义，会有人用XP电脑的，而且还是用自带的IE的那种。嗯 

一般来说，原则就是：**尽量支持XP，最低要求支持win7，开发网站时jQuery使用1.10.X版本，**
> If you need to support older browsers like Internet Explorer 6-8, Opera 12.1x or Safari 5.1+, use jQuery 1.12.(如果要支持旧的浏览器，比如IE6到IE8，Opera12.1X 或者Safari5.1+，你就用jQuery1.12)——官网说的


### 参考资料
* [browser support (jQuery官网)](http://jquery.com/browser-support/)
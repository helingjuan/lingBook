---
title: js-判断浏览器类型
tags: js
notebook: 前端
---
# js-判断浏览器类型
这个方法有很多，有一般的，也有巧妙的。
一般来说，是用这种方式：**通过navigator对象的appName属性或者是userAgent属性来判断浏览器类型**
navigator是window对象的一个属性，指向了一个包含浏览器相关信息的对象。

## 1. 浏览器类型说明
### 1.1 参数说明
- `appName` 返回当前浏览器内部“开发代号”名称。  
  就是要么返回Netscape，要么返回浏览器的全名，这是为了兼容性考虑的。
- `userAgent` 返回当前浏览器的用于HTTP请求的用户代理头的值。
  一般来说，这个值是由 `appCodeName + / + appVersion`组成，
  比如：Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36

举个例子： 
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191128112743.png)

#### 1.1.1 appName值说明(:-1:不推荐使用)
- IE和遨游浏览器Maxthon的appName 是`Microsoft Internet Explorer`
- FireFox和Opera的appName是 `Netscape`

从上面的图，我们可以发现，其实appName大部分都是`Netscape`(网景)，所以用这个来判断浏览器类型，是不太恰当的。

#### 1.1.2 userAgent值说明
- `micromessenger` 微信内置浏览器
- `iPhone|iPad|iPod|iOS` 就是苹果系的产品
- `Android` 就是安卓浏览器
- `msie && !opera` 就是IE  （？？？这个我看不懂了，为啥）
- `firefox` 火狐浏览器
- `chrome && webkit && mozilla` 就是谷歌浏览器
- `opera` 就是opera
- `webkit && !chrome && webkit && mozilla` 就是mac的Safari浏览器
## 2. js 判断浏览器类型和版本
概念大概理解了，其实代码就很清晰了。直接看吧。
其实这里有好几个场景的。
- 判断是移动端还是pc端
- 判断是安卓还是苹果
- 判断是火狐还是谷歌等等

### 2.1 判断是移动端还是pc端，移动端的话，是安卓还是苹果
```
var userBrowser = function() {
  var userAgent = window.navigator.userAgent.toLowerCase()
  // 通过正则来判断,match 或test都可以
  if()
}
```
### 2.2 判断当前是pc端哪个浏览器
```
/**
  * 判断当前是什么浏览器
  */
var userBrowser = function() {
  var userAgent = navigator.userAgent; //取得浏览器的userAgent字符串
  var isOpera = userAgent.indexOf("Opera") > -1; //判断是否Opera浏览器
  var isIE = userAgent.indexOf("compatible") > -1
          && userAgent.indexOf("MSIE") > -1 && !isOpera; //判断是否IE浏览器
  var isEdge = userAgent.indexOf("Edge") > -1; //判断是否IE的Edge浏览器
  var isFF = userAgent.indexOf("Firefox") > -1; //判断是否Firefox浏览器
  var isSafari = userAgent.indexOf("Safari") > -1
          && userAgent.indexOf("Chrome") == -1; //判断是否Safari浏览器
  var isChrome = userAgent.indexOf("Chrome") > -1
          && userAgent.indexOf("Safari") > -1; //判断Chrome浏览器

  if (isIE) {
      var reIE = new RegExp("MSIE (\\d+\\.\\d+);");
      reIE.test(userAgent);
      var fIEVersion = parseFloat(RegExp["$1"]);
      if (fIEVersion == 7) {
          return "IE7";
      } else if (fIEVersion == 8) {
          return "IE8";
      } else if (fIEVersion == 9) {
          return "IE9";
      } else if (fIEVersion == 10) {
          return "IE10";
      } else if (fIEVersion == 11) {
          return "IE11";
      } else {
          return "当前IE版本过低";
      }
  }
  if (isOpera) {
      return "Opera";
  }
  if (isEdge) {
      return "Edge";
  }
  if (isFF) {
      return "FireFox";
  }
  if (isSafari) {
      return "Safari";
  }
  if (isChrome) {
      return "Chrome";
  }
  
}
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191128175203.png)

## 参考资料
- [Navigator(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator)
- [JS如何判断浏览器类型，如何模拟浏览器类型（模拟微信浏览器）(博客园——南歌子)](https://www.cnblogs.com/nangezi/p/9342619.html)
- [javascript的navigator对象及属性userAgent(判断用户打开页面所处环境，如安卓或IOS)(CSDN——zxuanxuanz)](https://blog.csdn.net/qq_40542728/article/details/92652132)





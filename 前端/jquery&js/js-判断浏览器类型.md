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
* 判断当前是什么浏览器,仅pc端
* @return String 浏览器相关信息
*/
var userBrowser = function() {
  const userAgent = navigator.userAgent.toLowerCase() // 当前的用户代理,全都转化成小写
  let browserName = '' // 浏览器名称
  let browserVersion = userAgent.match(/(msie|firefox|chrome|opera|safari).*?([\d.]+)/) ?userAgent.match(/(msie|firefox|chrome|opera|safari).*?([\d.]+)/)[2] : '' // 浏览器版本
  let deviceName = '' // 设备名称
  let deviceMsg = '' // 设备具体信息
  let str = '' //最后结果
  if(/msie/i.test(userAgent) && !/opera/.test(userAgent)) { // IE 10及以下，用msie判断，IE11 就不行了
    browserName = 'IE 浏览器(Microsoft Internet Explorer)'
  } else if(/window/i.test(userAgent) && /trident/i.test(userAgent)) { // IE11 比较特殊，和IE10以下的都不一样，且和Edge也不一样
    browserName = 'IE 浏览器(Microsoft Internet Explorer)'
  } else if(/edg/i.test(userAgent)) {
    browserName = 'Edge浏览器(Microsoft Edge)'
  }else if(/firefox/i.test(userAgent)) {
    browserName = '火狐浏览器(Firefox)'
  } else if(/chrome/i.test(userAgent) && /webkit/i.test(userAgent) && /mozilla/i.test(userAgent)) {
    browserName = '谷歌浏览器(Chrome)'
  } else if(/opera/i.test(userAgent)) {
    browserName = '浏览器(opera)'
  } else if(/webkit/i.test(userAgent) &&!(/chrome/i.test(userAgent) && /webkit/i.test(userAgent) && /mozilla/i.test(userAgent))) {
    browserName = 'Safari浏览器(Safari)'
  } else {
    browserName = '不知道的浏览器'
  }
  // 获取平台信息
  let firstIndex = userAgent.indexOf('(')
  let deviceEndIndex = userAgent.indexOf(';')
  let endIndex = userAgent.indexOf(')')
  deviceName = userAgent.substr(parseInt(firstIndex)+1,parseInt(deviceEndIndex)-parseInt(firstIndex))
  deviceMsg = userAgent.substr(parseInt(firstIndex),parseInt(endIndex)-parseInt(firstIndex)+1)


  str = '我是<strong>PC端</strong>，' + browserName + '<br/> 当前所在：<strong>' + deviceName + '</strong><br/> 其平台信息：'+ 
  deviceMsg + '<br/> 其浏览器版本：<strong>' + browserVersion + '</strong><br/> 具体是：' + userAgent
  if(isWeChat) {
    str += '<br>是微信内置浏览器'
  } else {
    str += '<br>不是微信内置浏览器'
  }
  return str
}
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191128175203.png)
### 2.3 判断是否是微信内置浏览器
如果不知道怎么在chrome浏览器模拟微信浏览器，可以看下这个[用Chrome模拟其它的浏览器，比如微信浏览器](https://github.com/heihuahe/lingBook/blob/master/%E5%B7%A5%E5%85%B7%E6%95%99%E7%A8%8B/chrome/%E7%94%A8Chrome%E6%A8%A1%E6%8B%9F%E5%85%B6%E5%AE%83%E7%9A%84%E6%B5%8F%E8%A7%88%E5%99%A8%EF%BC%8C%E6%AF%94%E5%A6%82%E5%BE%AE%E4%BF%A1%E6%B5%8F%E8%A7%88%E5%99%A8.md)
```
/**
  * 判断当前环境是否是微信内置浏览器
  * 有两种实现方式，match和test,这里用的是test方法
  * @return true/false true的话，就是微信浏览器
  */
var isWeChatBrowser = function() {
  var userAgent = navigator.userAgent.toLowerCase(),
      regStr  = new RegExp('/micromessenger/i');
  return regStr.test(userAgent)
}
```
```
/**
  * 判断当前环境是否是微信内置浏览器
  * 有两种实现方式，match和test,这里用的是match方法
  * match() 会返回一个数组，所有匹配到的值，如果没有匹配到，就会返回空null
  * @return true/false true的话，就是微信浏览器
  */
var isWeChatBrowserMatch = function() {
  var userAgent = navigator.userAgent.toLowerCase();
  if(userAgent.match(/Micromessenger/i) == 'micromessenger') {
    return true
  } else {
    return false
  }
}
```
### 2.4 统一判断，既判断PC端，又判断移动端(我自己测试过的)
```
/**
   * 浏览器判断，
   * pc端：就是知道具体是哪个浏览器，
   * 移动端：就知道是哪个系统的，安卓还是苹果，再判断是否是微信内置浏览器
   * macth 有个问题，如果找不到，容易报错，然后就中止了。
   */
  var browserJudge = function() {
    const userAgent = navigator.userAgent.toLowerCase() // 当前的用户代理,全都转化成小写
    let isMobile = false // 是否是移动端
    let isWeChat = false // 是否是微信内置浏览器
    let browserName = '' // 浏览器名称
    let browserVersion = userAgent.match(/(msie|firefox|chrome|opera|safari).*?([\d.]+)/) ?userAgent.match(/(msie|firefox|chrome|opera|safari).*?([\d.]+)/)[2] : '' // 浏览器版本
    let deviceName = '' // 设备名称
    let deviceMsg = '' // 设备具体信息
    let str = '' //最后结果

    // 判断移动端浏览器
    if(/(iphone|ipad|ipod|ios)/i.test(userAgent)) { // 是否是苹果
      isMobile = true
      browserName = 'Safari浏览器(iOS)'
    } else if(userAgent.match(/(android).*?([\d.]+)/) && userAgent.match(/(android).*?([\d.]+)/)[1] === 'android') { // 安卓,因为安卓的一般都会带上版本，test检测不出来，match可以
      isMobile = true
      browserName = '安卓浏览器(Android)'
    } else {
      isMobile = false
    }
    // 是否是微信内置浏览器
    if(isMobile) {
      if(/(microMessenger)i/.test(userAgent)) {
        isWeChat = true
      } else {
        isWeChat = false
      }
      if(/firefox/i.test(userAgent)) {
        browserName = '火狐浏览器(Firefox)'
      } else if(/chrome/i.test(userAgent) && /webkit/i.test(userAgent) && /mozilla/i.test(userAgent)) {
        browserName = '谷歌浏览器(Chrome)'
      }
    }
    // 判断pc端浏览器
    if(!isMobile) {
      if(/msie/i.test(userAgent) && !/opera/.test(userAgent)) { // IE 10及以下，用msie判断，IE11 就不行了
        browserName = 'IE 浏览器(Microsoft Internet Explorer)'
      } else if(/window/i.test(userAgent) && /trident/i.test(userAgent)) { // IE11 比较特殊，和IE10以下的都不一样，且和Edge也不一样
        browserName = 'IE 浏览器(Microsoft Internet Explorer)'
      } else if(/edg/i.test(userAgent)) {
        browserName = 'Edge浏览器(Microsoft Edge)'
      }else if(/firefox/i.test(userAgent)) {
        browserName = '火狐浏览器(Firefox)'
      } else if(/chrome/i.test(userAgent) && /webkit/i.test(userAgent) && /mozilla/i.test(userAgent)) {
        browserName = '谷歌浏览器(Chrome)'
      } else if(/opera/i.test(userAgent)) {
        browserName = '浏览器(opera)'
      } else if(/webkit/i.test(userAgent) &&!(/chrome/i.test(userAgent) && /webkit/i.test(userAgent) && /mozilla/i.test(userAgent))) {
        browserName = 'Safari浏览器(Safari)'
      } else {
        browserName = '不知道的浏览器'
      }
    }
    // 获取平台信息
    let firstIndex = userAgent.indexOf('(')
    let deviceEndIndex = userAgent.indexOf(';')
    let endIndex = userAgent.indexOf(')')
    deviceName = userAgent.substr(parseInt(firstIndex)+1,parseInt(deviceEndIndex)-parseInt(firstIndex))
    deviceMsg = userAgent.substr(parseInt(firstIndex),parseInt(endIndex)-parseInt(firstIndex)+1)

    if(isMobile) {
      str = '我是<strong>移动端</strong>，' + browserName + '<br/> 当前所在：<strong>' + deviceName + '</strong><br/> 其平台信息：'+ 
      deviceMsg + '<br/> 其浏览器版本：<strong>' + browserVersion + '</strong><br/> 具体是：' + userAgent
    } else {
      str = '我是<strong>PC端</strong>，' + browserName + '<br/> 当前所在：<strong>' + deviceName + '</strong><br/> 其平台信息：'+ 
      deviceMsg + '<br/> 其浏览器版本：<strong>' + browserVersion + '</strong><br/> 具体是：' + userAgent
    }
    if(isWeChat) {
      str += '<br>是微信内置浏览器'
    } else {
      str += '<br>不是微信内置浏览器'
    }
    return str
  }
```
## 参考资料
- [Navigator(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator)





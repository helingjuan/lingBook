---
title: js- window.event.witch 谷歌浏览器和火狐的回车事件
tags:
notebook:
---
# js- window.event.witch 谷歌浏览器和火狐的回车事件
## 概述
场景：**用扫码枪扫二维码**

扫码枪自带回车，所以只要监控回车那个参数，然后调用方法就可以。

但是出现了一个问题：
**火狐 的参数是window.event.witch == 13, 但是谷歌就不一定了，什么参数都有可能，出现过229， 16等。那么在谷歌浏览器怎么监控这个参数啊？（下图是谷歌的回车打印参数）**
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552028565095.png)


## 问题分析
努力解决，先获取一些基本资料
### 1.什么是扫码枪？
——扫码枪本质上来件是一种输入设备，和键盘没有任何区别

这个示例，只对火狐的浏览器管用，谷歌不能自动调用方法
```
//html
 <form class="form-horizontal" action="" method="" onkeydown="if(event.keyCode == 13)return false;">
    <div class="row-fluid margin-top-20">
        <input type="text" name="input" id="activity_code" placeholder="请输入报名编号" class="wrap margin-right-10" onkeyup="mm.action(this, event)" autocomplete="off">
        <button type="button" class="btn blue" onclick="mm.activityVerification(this)">检 录</button>
    </div>
    <div id="result_content" class="result row-fluid margin-top-20"></div>
</form>
```

```
// js
mm.action = function(tag, e) {
    var ev = e || window.event;
    if(ev.which == 13){
      mm.activityVerification(tag)
    }
  }
```
## 解决办法

不建议使用which，这是即将被废弃的属性。
推荐使用keyCode

## 参考资料
- [javascript扫码枪的判断输入 (CSDN-洋蒸鱼)](https://blog.csdn.net/phoenix_shine/article/details/70245444)
- [js获取键盘按下的键值event.keyCode,event.charCode,event.which的兼容性 (bbsmax-风雨后见彩虹)](https://www.bbsmax.com/A/obzblOB5ED/)





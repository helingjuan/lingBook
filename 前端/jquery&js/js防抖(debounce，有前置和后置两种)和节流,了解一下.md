---
title: js防抖(debounce，有前置和后置两种)和节流(throttling),了解一下
tags: js
notebook: js
---
# js防抖(debounce，有前置和后置两种)和节流,了解一下
### 需求背景
在工作中，遇到了用户多次点击按钮，重复提交表单的情况。就是可能一个双击就提交了两次请求，这样就会对用户的使用造成很大的困扰。所以我们就采用防抖来控制一下吧。

### 防抖和节流的简介
这两种都

### 防抖
```
// 后置防抖
var debounce = function(fn, time) {
      var timeout = ''
      return function() {
        var self = this
        //清除上一个定时器
        if (timeout){
          clearTimeout(timeout);
        } 
        if (!timeout){
          fn.call(self, arguments);
        } 
        //创建一个新的定时器 时间间隔1s
        timeout = setTimeout(function() {
          timeout = ''
        }, time);
      }
    }
    var fn = debounce(addVisitorAction, 1500)
    mm.addVisitor = function() {
      fn()
    }
```

### 节流

### 参考资料


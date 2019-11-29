---
title: js-监听键盘事件
tags: 
notebook: 前端
---
# js-监听键盘事件
点击一个键盘的事件流程：**keydown -> keypress -> keyup**  
看个代码：
```
//键盘操作 
// 同时监听keyup和paste事件 
$("#" + that.options.searchBox).on('keyup paste',function (event) {
    //处理键盘操作
    var myEvent = event || window.event;
    var keyCode = myEvent.keyCode;
    if (keyCode == 38) { //向上
        // 操作
    }else if (keyCode == 40) { //向下
        // 操作
    }else if (keyCode == 13) { //回车键
        // 操作
    } else {
        timer = myEvent.timeStamp;   //利用event的timeStamp来标记时间，这样每次的keyup事件都会修改timer的值，注意timer必需为全局变量
        setTimeout(function() {
            if(timer - myEvent.timeStamp == 0){  //如果时间差为0（也就是你停止输入0.5s之内都没有其它的keyup事件发生）则做你想要做的事
                if (!that.ignoreSpaces($("#" + that.options.searchBox).val())) {
                    // 输入为空字符串时，不做操作
                    $("#" + that.options.autoId).hide();
                } else {   //有文字输入时获取提示词
                    that.autoComplete();
                }
            }
        }, 300);
    }
});
```

### 监听keydown事件
```
// 方法1
$("#id").keydown(function(event) {

})
// 方法2
$("#id").on('keydown', function(event) {

})
```

### 监听keyup事件
```
// 方法1
$("#id").keyup(function(event) {

})
// 方法2
$("#id").on('keyup', function(event) {

})
```


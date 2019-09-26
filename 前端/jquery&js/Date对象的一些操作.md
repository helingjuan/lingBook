---
title: Date对象的一些操作
tags: 
notebook: 
---
# Date对象的一些操作
### 计算两个日期之间的天数差
```
var dateStart = new Date("2019-08-01");
var dateEnd = new Date("2019-08-12");
var days = (dateEnd - dateStart) / (1000 * 60 * 60 * 24));
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190812152646.png)

### 格式转换：20190828 转换成 2019-08-28
方法1：正则
```
'20190828'.replace(/^(\d{4})(\d{2})(\d{2})$/, "$1-$2-$3"),
```
效果：    
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190828144848.png)

### 格式装换：时间戳 转换成2019/08/28
```
//时间戳转换
var timeFormat = function(timeStamp) {
  var timeStr = new Date();
  timeStr.setTime(timeStamp *1000);
  timeStr = timeStr.toLocaleDateString(); //输出 2018/5/17 格式
  return timeStr;
}
```

### 获取当天日期：格式：2019-09-09
```
var getDate = function() {
    var date = new Date()
    var yyyy = date.getFullYear()
    var mm = (date.getMonth() +1) < 10 ? '0'+(date.getMonth() +1) : date.getMonth() +1;
    var dd = date.getDate() < 10 ? '0' +date.getDate() : date.getDate()
    return yyyy + '-' + mm + '-' + dd
  }
```

### 时间累加，一秒秒加
```
var nowDate = ''
    // 获取后台的时间
    mm.apiAjax({
      url: path.u('/index/index/getNowDate'),
      success: function(res) {
        nowDate = new Date(res.date_now)
      }
    })
    //获取系统时间，将时间以指定格式显示到页面
    var timer = setInterval(function(){
        //获取系统时间。
        
        // var now = new Date();
        var now = nowDate
        var y = now.getFullYear(),
            month = now.getMonth() + 1,
            d = now.getDate(),
            h = now.getHours(),
            minutes = now.getMinutes(),
            s = now.getSeconds();
        month = month >= 10 ? month : '0' + month;
        d = d >= 10 ? d : '0' + d;
        h = h >= 10 ? h : '0' + h;
        minutes = minutes >= 10 ? minutes : '0' + minutes;
        s = s >= 10 ? s : '0' + s;
        //将时间显示到ID为time的位置，时间格式形如：19:18:02
        $("#sys_time").html(y + '-' + month + '-' + d + '  ' + h + ':' + minutes + ':' + s);
        // 敲重点！！！
        nowDate = new Date(y,now.getMonth(),d,h,minutes,s+1)
    },1000)
```
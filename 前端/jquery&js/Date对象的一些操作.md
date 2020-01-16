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
### 上月日期
```
var date=new Date(year,month,0); 就是月初的前一天，就是上月月底的那天
```

### 各种日期范围的获取
```
/**
   * 日期格式化 yyyy-mm-dd
   * @param timeStamp 时间戳
   */
  formatByTimeStamp(timeStamp: number) {
    const date = new Date(timeStamp)
    return this.formatByDate(date)
  }
  /**
   * 日期格式化 yyyy-mm-dd
   * @param timeStamp 时间戳
   * @returns yyyy-mm-dd 字符串
   */
  formatByDate(date: Date) {
    const year = date.getFullYear()
    const monthTemp = date.getMonth() + 1
    const month = monthTemp < 10 ? '0' + monthTemp : monthTemp
    const day = date.getDate() < 10 ? '0' + date.getDate() : date.getDate()
    return year + '-' + month + '-' + day
  }
  /**
   * 获取日期范围
   * @param dateObj 日期参数
   */
  getDateRange(dateObj: dateParam) {
    const date =  new Date()
    const dayOfWeek = date.getDay() // 本周的第几天
    const year = date.getFullYear() // 年
    const month = date.getMonth() // 月，从0开始--- 11 就是12月份
    const day = date.getDate() // 当前日，本月的第几天
    const dayTimestamp: number = 24 * 60 * 60 * 1000 // 一天的时间戳
    let startDate = new Date()
    let endDate = new Date()
    switch(dateObj.dateTag) {
      case 'today': // 今天
        this.start_date = this.formatByDate(date)
        this.end_date = this.start_date
        break
      case 'yesterday': // 昨天
        this.start_date = this.formatByTimeStamp(date.getTime() - dayTimestamp)
        this.end_date = this.start_date
        break
      case 'severalDays': { // 最近几天
        if (dateObj.dayNum) {
          const startDate = date.getTime() - (dateObj.dayNum - 1) * dayTimestamp
          this.start_date = this.formatByTimeStamp(startDate)
          this.end_date = this.formatByDate(date)
        }
        break
      }
      case 'week': // 本周
        this.start_date = this.formatByTimeStamp(date.getTime() - (dayOfWeek - 1) * dayTimestamp)
        this.end_date = this.formatByDate(date)
        break
      case 'lastWeek': {// 上周
        const lastWeekEndDay = date.getTime() - (day - dayOfWeek - 1) * dayTimestamp // 上周结束的日期
        this.start_date = this.formatByTimeStamp(lastWeekEndDay - 6 * dayTimestamp) // 上周开始的日期
        this.end_date = this.formatByTimeStamp(lastWeekEndDay)
        break
      }
      case 'lastMonth': {  // 上个月
        let lastMonthStart = new Date()
        if (month === 0) { // 如果是一月份，就跨年了
          lastMonthStart = new Date(year - 1, 11, 1) // 上个月, 月份是从0开始的，所以11 就是12月
        } else {
          lastMonthStart = new Date(year, month - 1, 1)
        }
        this.start_date = this.formatByDate(lastMonthStart)
        this.end_date = this.formatByDate(new Date(year, month, 0)) // 上个月月底
        break
      }
    }

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
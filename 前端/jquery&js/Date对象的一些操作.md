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
---
title: bootstrap datepicker使用介绍
tags: 插件
notebook: 前端
---

# bootstrap datepicker使用介绍
### 初始化
```
<div class="input-append date datepicker margin-left-10">
  <input class="m-wrap small form-control" type="text" value="" id="time_start" name="time_start" readonly/>
  <span class="add-on"><i class="fa fa-calendar"></i></span>
</div>
-
<div class="input-append date datepicker">
  <input class="m-wrap small form-control" type="text" value="" id="time_end" name="time_end" readonly/>
  <span class="add-on"><i class="fa fa-calendar"></i></span>
</div>
```
```
// js
$(".datepicker").datepicker({
    language: "zh-CN",
    autoclose: true,
    format: "yyyy-mm-dd",
    weekStart: 0,
    todayBtn: true
});
```
### 1.控件支持手输
其实就是去掉input框的readonly属性。
```
<div class="input-append date datepicker margin-left-10">
  <input class="m-wrap small form-control" type="text" value="" id="time_start" name="time_start" />
  <span class="add-on"><i class="fa fa-calendar"></i></span>
</div>
-
<div class="input-append date datepicker">
  <input class="m-wrap small form-control" type="text" value="" id="time_end" name="time_end" />
  <span class="add-on"><i class="fa fa-calendar"></i></span>
</div>
```

### 2.设置日期控件时间
有2种方法：1.通过datepicker插件的方法；2.直接设置input的值  
**前提：格式都得正确！**
```
// 方法1 通过datepicker插件的方法
$("#time_start").datepicker('setDate',lastWeek);
```
```
// 方法2 直接设置input的值
$("#time_start").val(lastWeek)
```



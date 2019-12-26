---
title: js-radio的一些操作
tags: js
notebook: 前端
---
# js-radio的一些操作
## 概述
老忘老忘，气死个人
<!-- TOC -->

- [js-radio的一些操作](#js-radio的一些操作)
  - [概述](#概述)
  - [1. 监听](#1-监听)
    - [1.监听所有单选按钮，然后通过值的不同，进行相关操作](#1监听所有单选按钮然后通过值的不同进行相关操作)
    - [2. 监听单个按钮，如果它被选中了，就进行相关操作](#2-监听单个按钮如果它被选中了就进行相关操作)

<!-- /TOC -->
## 1. 监听

### 1.监听所有单选按钮，然后通过值的不同，进行相关操作
举个例子：

``` html
<div id="status">
  <label>
    <input type="radio" name="status" value="1" checked>有效
  </label>
  <label>
    <input type="radio" name="status" value="0">无效
  </label>
</div>
```
``` javascript
$("#status :radio").change(function(){
  var status = $(this).val()
  // 找其中的某一个元素 find
  var time = $(this).find("#time").val()
})
```

### 2. 监听单个按钮，如果它被选中了，就进行相关操作
举个例子：比如我们要监听那个有效的按钮

``` javascript
$("#status :radio").change(function(){
  var status = $(this).val()
  if(status === '1') {
    console.log('你现在可以做一些操作了')
  }
})




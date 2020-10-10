---
title: js 判断参数是否为对象
tags: js  
notebook: 前端
---
# js 判断参数是否为对象
<!-- TOC -->

- [js 判断参数是否为对象](#js-%E5%88%A4%E6%96%AD%E5%8F%82%E6%95%B0%E6%98%AF%E5%90%A6%E4%B8%BA%E5%AF%B9%E8%B1%A1)
  - [1. toString():+1:](#1-tostring1)
  - [2. instanceof](#2-instanceof)
  - [3. typeof](#3-typeof)
  - [4. $.isPlainObject() 是否是纯粹的对象](#4-isplainobject-%E6%98%AF%E5%90%A6%E6%98%AF%E7%BA%AF%E7%B2%B9%E7%9A%84%E5%AF%B9%E8%B1%A1)
  - [5. constructor](#5-constructor)
  - [参考资料](#%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)

<!-- /TOC -->
## 1. toString():+1:
```
Object.prototype.toString.call(res[i]) == '[object Object]'// 注意，第二个Object首字母大写！
```

## 2. instanceof 
这里需要注意一点，因为**数组也是对象**，所以遇到数组的时候，也是返回true
```
obj instanceof Object // 是对象就返回 true,不是就false
```

## 3. typeof
这个有上面的instanceof一样的问题，没法区分数组和对象，而且null 也是Object
```
typeof obj === Object
```
具体看表格：
| 表达式 | 返回值 |
| --- | --- | 
| typeof undefined | 'undefined' | 
| typeof null | 'object' | 
| typeof true | 'boolean' | 
| typeof 15 | 'number' | 
| typeof 'hhh' | 'string' | 
| typeof function(){} | 'function' | 
| typeof [] | 'object' | 
| typeof {} | 'object' | 

## 4. $.isPlainObject() 是否是纯粹的对象
什么是纯粹的对象？
就是对象是通过`{}`或者 `new Obejct` 声明的。  
适用于jQuery
这个函数属于全局jQuery对象
```
$.isPlainObject(obj) 
// 返回值为Boolean
```
## 5. constructor
```
obj.constructor === Object
```
## 参考资料
- [Object.prototype.toString()(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

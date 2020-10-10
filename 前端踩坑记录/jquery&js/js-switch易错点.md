---
title: js-swicth易错点
tags: js
notebook: 前端
---
# js-swicth易错点
<!-- TOC -->

- [js-swicth易错点](#js-swicth%e6%98%93%e9%94%99%e7%82%b9)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [javascript里的switch](#javascript%e9%87%8c%e7%9a%84switch)
  - [其他语言里的switch](#%e5%85%b6%e4%bb%96%e8%af%ad%e8%a8%80%e9%87%8c%e7%9a%84switch)
    - [c语言](#c%e8%af%ad%e8%a8%80)
    - [java](#java)

<!-- /TOC -->
## 概述
因为switch算是一个比较通用，常见的方法，所以有时候会记混了。

## javascript里的switch
注意！！！
javascript 里，**switch的条件可以是任意类型**，比如`int`，`string`(划重点！！！一直记错以为不可以，其实是可以的)

## 其他语言里的switch
### c语言
只支持int类型。

### java
在`java 7` 之前，swicth都是只能int类型的。
在`java 7`及之后的版本，switch提供了对string类型的支持。




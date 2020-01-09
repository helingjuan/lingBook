---
title: Eslint报错：no-case-declarations
tags: eslint
notebook: 前端
---
# Eslint报错：no-case-declarations
<!-- TOC -->

- [Eslint报错：no-case-declarations](#eslint%e6%8a%a5%e9%94%99no-case-declarations)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [错误示范](#%e9%94%99%e8%af%af%e7%a4%ba%e8%8c%83)
  - [解决方法](#%e8%a7%a3%e5%86%b3%e6%96%b9%e6%b3%95)
  - [参考资料](#%e5%8f%82%e8%80%83%e8%b5%84%e6%96%99)

<!-- /TOC -->
## 概述
就是在switch语句中，声明了变量，然后引起的报错。
看下解释：
> 该规则禁止词法声明（let，const，function和class在）case/ default条款。原因是词法声明在整个开关块中是可见的，但只有在分配时才会被初始化，这只有在达到定义它的情况下才会发生。

所以！要确保词法声明仅适用于当前case子句，请将子句包装在块中。
## 错误示范
```
swicth(type) {
  case 1:
    let temp = ''
    break
  case 2:
    console.log('hhhh')
    break
  case 3:
    let arrayTemp = []
    break
}
```
可能存在的问题：
就是在case里声明的变量是在switch语句块内都有效的，这样就有可能出现变量作用域不对的问题，使得，case1的临时变量temp 在case2 和case 3 中都可以访问的到。
## 解决方法
```
swicth(type) {
  case 1: {
    let temp = ''
    break
  }
  case 2:
    console.log('hhhh')
    break
  case 3: {
    let arrayTemp = []
    break
  }
}
```
总结： 就是在要声明变量的case语句块里加大括号，这样就不会出现报错和其他问题
## 参考资料
- [eslint:no-case-declarations(我是前端-Jerman)](https://www.imqianduan.com/eslint/180.html)
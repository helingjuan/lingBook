---
title: Eslint 报错：Do not access Object.prototype method 'hasOwnProperty' from target object
tags: eslint
notebook: 前端
---
# Eslint 报错：Do not access Object.prototype method 'hasOwnProperty' from target object
## 具体报错
```
Do not access Object.prototype method 'hasOwnProperty' from target object (no-prototype-builtins)
```
这就是说，不能直接使用对象原型上的方法，因为原型上的方法可能被重写了。
## 错误示范
```
// sheetTempObj.data[m] 是个对象
// heardName 就是属性名
(sheetTempObj.data[m]).hasOwnProperty(heardName)
```
## 正确示范
```
// sheetTempObj.data[m] 是个对象
// heardName 就是属性名
Object.prototype.hasOwnProperty.call(sheetTempObj.data[m], heardName)
```
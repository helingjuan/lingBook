---
title: 获取对象的属性数 getOwnPropertyNames(object)
tags: js
notebook: 前端
---
# 获取对象的属性数 getOwnPropertyNames(object)
## 概述
就有时候，你需要知道这个对象大小（属性的数量），但是对象又没有直接的属性来获取这个（比如数据的length），所以就需要通过其它方式来获取。看看吧
## getOwnPropertyNames(object).length
> `getOwnPropertyNames(object)` 这个可以获取对象所有属性的**数组**
> 所以就可以通过数组的方式获取到属性值数量了。

举个例子：

```
var foo = {a1:'1',a2:'2',a3:'3'};

//获得对象所有属性的数组
Object.getOwnPropertyNames(foo);
> [ 'a1', 'a2', 'a3' ]

//获取对象属性的个数
Object.getOwnPropertyNames(foo).length;
> 3
```

## 参考资料
- [在javascript中获取一个对象内属性的个数(博客园-白色的海)](https://www.cnblogs.com/kongxianghai/p/6640733.html)

---
title: TypeScript学习三：变量声明
tags: typescript
notebook: 前端
---
# TypeScript学习三：变量声明
## 1.概述
在原生javascript中，我们一般使用var来声明变量，因为var 声明的变量会出现变量提升的情况，所以后来出现了let和const等命名方式。这里也是主要介绍这三种变量的声明。  
这里必不可少的是了解**这3者（var、let、const）的区别**：
- 变量作用域
  - var 声明的变量是全局的或者函数块的；
  - let和const 声明的变量是块级的变量；
- 是否会变量提升
  - var 声明的变量存在变量提升
  - let和const 声明的变量不存在变量提升
- 是否可以重新赋值
  - var和let 声明的变量可以重新赋值
  - const 声明的变量不允许重新赋值
- 是否可以只声明变量不赋值
  - var和let 可以，这时候默认赋值undefined
  - const 不行，会报语法错误，缺少初始化
- 是否可以重复声明变量？
  - var 可以
  - let和const不行，因为使用let和const声明的变量在该作用域内是唯一的，不可以重复声明。
## `var`声明
重点就在var的作用域范围上。看几个例子：
```
// 例子1
function f() {
  var a = 10
  return function add() {
    var b = a + 1
    return b
  }
}
var number = f(); // f() return add()函数，所以number 是个函数，== add()
number()  // 调用add()函数 return b = 11
```
效果：![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191105162222.png) 
这里就是一个知识点：**var声明的变量，在函数内部定义了，那么在其他函数内部也可以访问相同的变量**
上面的例子就是，a 是f函数里声明的变量，b是add函数里声明的变量。add函数可以获取到f函数的a变量。即使当add在f已经执行完毕后才被调用，它仍然可以访问及修改a变量(这句话我就不怎么理解了。。。总觉得没什么必要)

```
// 例子2
function work(isWord: boolean) {
  if(isWord) {
    var x = 10;
  }
  return x;
}
work(true); // return x = 10
work(false); // 变量x未声明，所以return x其实是做了2步，声明x和return x，因为x只声明没赋值，所以x是undefined
```
这里其实能很明显看出var 的作用域了，用多了var 一看，就觉得理所当然可以访问到x变量，没什么可犹豫的。但是其实，这个就和其他语言的变量作用域有很大的区别。
**其他语言：大多数是块作用域**，就比如这个x，在if里声明了，那么就只有if-else这个判断里能获取到x，return x 就是undefined了；
**在javascript里：函数作用域**，在函数里任意一个地方声明的变量，在整个函数作用域内都可以获取到，所以return 10
### 缺点
但是！！！！有个问题，这个**作用域范围太大了！！而且还不校验变量的唯一性**（就是可以多次声明同一个变量。。。）
然后就容易出现重复命名一个参数的情况，而这些参数是在相同的函数作用域内，就会发生一些意想不到的bug，还很难找出来。。。   
举个例子   
```
function sumMatrix(matrix: number[][]) {
    var sum = 0;
    for (var i = 0; i < matrix.length; i++) {
        var currentRow = matrix[i];
        for (var i = 0; i < currentRow.length; i++) {
            sum += currentRow[i];
        }
    }

    return sum;
}
```
这里的i就是重复声明的变量，然后就会取错数据 哈哈哈哈哈哈哈  真的是太惨了
千万别这么干！！！！
还有一种常见的问题（非常容易错！！！，认真看）
```
for(var i = 0; i< 10; i++) {
  setTimeout(function() {
    console.log(i)
    }, 100 * i)
}
// 结果：输出10次 都是10 （惊不惊喜！意不意外！）
```
setTimeout 就是在 100 *i 毫秒后，执行function
我们理想的输出是： 0 1 2 3 4 5 6 7 8 9 
但是现实的输出是：10 10 10 10 10 10 10 10 10 10
那这是为什么呢？？？  
这里应该是个函数作用域，所以每个i都是指向同一个函数作用域里的i，而在for循环中使用setTimeout，这就涉及到了异步机制（这又是另一个知识点了：**JS的运行机制**）
简单解释一下：因为JS是单线程环境，就是代码的执行是从上到下，一步步来的，就是同步，需要排队；而异步是指不进入主线程，进入任务队列的任务。只有接到通知可以执行了，这个任务才会进入主进程。最关键的一点：**在所有同步任务执行完之前，任何的异步任务是不会执行的**。
**常见的异步任务**有：
1. setTimeout 和 setInterval
2. DOM事件
3. ES6的Promise
4. Ajax异步请求

而setTimeout就是一个异步任务，所以就要等for循环执行完(i=10时)，才会执行。

还有一种情况：
```
for(var i= 0; i < 10; i++) {
  setTimeout(console.log(i), 0)
}
// 结果： 0 1 2 3 4 5 6 7 8 9
```
上面说了，setTimeout是等所有同步任务执行完了才执行，那为什么不一样呢？
这就涉及到了console.log 和 console.log() 的区别了。
- console.log 这是一个立即执行函数
- console.log() 这是一个觉console.log的函数，是同步任务，和for循环同步执行。

所以结果就是那样啦。

那么还有一种情况：
```
for(var i=0;i<10;i++){
     setTimeout("console.log(i)",1000);//连续的10个10
 }
```
这是因为加了双引号的console.log() 不再是立即执行函数，setTimeout 会判断第一个参数是否是函数，如果不是，则会尝试将它当做字符串处理，就是说，console.log(i)执行后的返回值转为字符串。（真是太复杂了）


## 参考资料
- [TypeScript官方文档](https://www.tslang.cn/docs/handbook/variable-declarations.html)
- [TypeScript英文文档](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md)
- [javascript中var、let、const声明的区别(segmentfault——fanqifeng)](https://segmentfault.com/a/1190000012221834)
- [在for循环中运行setTimeout的三种情况(CSDN——我升4级啦啦啦)](https://blog.csdn.net/Febby_/article/details/94763441)


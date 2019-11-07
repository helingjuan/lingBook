---
title: TypeScript学习三：变量声明
tags: typescript
notebook: 前端
---
# TypeScript学习三：变量声明
<!-- TOC -->

- [TypeScript学习三：变量声明](#typescript学习三变量声明)
  - [1.概述](#1概述)
  - [`var`声明](#var声明)
    - [缺点](#缺点)
  - [let 声明](#let-声明)
    - [作用域：块作用域](#作用域块作用域)
    - [重定义及屏蔽](#重定义及屏蔽)
    - [块级作用域变量的获取](#块级作用域变量的获取)
  - [const声明](#const声明)
  - [解构](#解构)
    - [1. 解构数组](#1-解构数组)
    - [2.对象解构](#2对象解构)
  - [展开](#展开)
    - [1. 展开数组](#1-展开数组)
    - [2. 展开对象](#2-展开对象)
  - [参考资料](#参考资料)

<!-- /TOC -->
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
那么回到第一种情况，我们怎么解决那个输出结果不对的问题呢？
可以这么干：**使用立即执行的函数表达式来捕获每次迭代时i的值**
举个例子：  
```
for(var i = 0; i< 10; i++) {
  (function(i){
    setTimeout(function(){
      console.log(i)
    }, 100*i)
  })(i)
}
结果： 0 1 2 3 4 5 6 7 8 9
```
这样就可以正确输出啦！

## let 声明
let与var 的写法一致，主要区别在语义和作用域范围上。
### 作用域：块作用域
它的作用域是词法作用域或块作用域。**只能在包含它们的块或for循环内访问**。
举个例子：  
```
function add(input: boolean) {
  let a = 100;
  if(input) {
    let b = a + 1 //a 是可以访问到的
    return b
  }
  return b // 报错：b不存在
}
```
从这里可以很明显的看出来a和b的作用域范围：a是add函数内，b是if语句块里。
除此之外，let还有一个特点：**不能在被声明之前读或写**。虽然这些变量始终存在于他们的作用域里，但是在直到声明它的代码之前，之前的区域都属于**暂时性死区**。
还有一个要注意：**我们可以在一个拥有块作用域变量被声明前获取它，只是不能在变量声明前去调用这个函数。**
举个例子：  
```
function foo() {
  return a // a 在函数foo里未定义
}
foo() // 调用函数foo，此时会报错，因为a未定义
let a // 声明变量a
```
### 重定义及屏蔽
上面var声明提到，var声明如果重名的话，是不会报错的，且指向同一个作用域，就是只会得到一个值。但是到let这里就不一样了。**let变量在一个作用域里的声明是唯一**，就是不能出现重名的变量，否则会报错的。
举个例子： 
```
let name = "lucky"
let name = "lucy" // 报错，name变量已经声明过了
```
此外，在一个嵌套作用域里引入一个新名字的行为叫做**屏蔽**。！注意：这个有可能会不小心地引入新问题,同时也可能会解决一些错误。
举个例子：
```
function sumMatrix(matrix: number[][]) {
    let sum = 0;
    for (let i = 0; i < matrix.length; i++) {
        var currentRow = matrix[i];
        for (let i = 0; i < currentRow.length; i++) {
            sum += currentRow[i];
        }
    }

    return sum;
}
// 这个就可以正确的输出，因为内层循环的i可以屏蔽掉外层循环的i
```
即使如此，还是**不建议使用屏蔽**，容易混乱。
### 块级作用域变量的获取
先看看函数作用域的var的变量是怎样的吧，
简单的说，每次进入一个作用域时，var 声明变量，创建一个变量的环境，然后获取变量，但是当作用域内的代码执行完毕后，这个变量和变量环境依然存在。
上面说到同步任务(for循环)和异步任务(setTimeout)在一起使用的问题，需要使用立即执行的函数表达式来获取每次for循环里的状态，而这个的本质就是**为获取到的变量创建一个新的变量环境**
而let声明在循环体力就拥有完全不同的情况。它不仅仅是在循环里引入了一个新的变量环境，而是**针对每次循环**都会创建这样一个新作用域。所以let声明就可以解决var的痛点。
举个例子：  
```
for(let i = 0; i < 10; i++) { // 注意！是let声明
  setTimeout(function(){
    console.log(i)
  }, 100 * i)
}
//结果： 0 1 2 3 4 5 6 7 8 9
```

## const声明 
const声明是声明变量的另一种方式，他是let的升级版，**拥有和let相同的作用域规则，但是不能对它们重新赋值**。但是如果你是对象类型的话，其实是可以修改的。
举个例子：  
```
const numLivesForCat = 9;
const kitty = {
    name: "Aurora",
    numLives: numLivesForCat,
}

// Error
kitty = {
    name: "Danielle",
    numLives: numLivesForCat
};

// all "okay"
kitty.name = "Rory";
kitty.name = "Kitty";
kitty.name = "Cat";
kitty.numLives--;
```
这时候就需要用特殊的方式去避免，**TypeScript允许将对象的成功设置成只读的**。

## 解构
解构就是可以把数组拆解出来声明成一个个变量，可以把对象的属性拆解出来声明成一个个变量。
### 1. 解构数组
最简单的解构。
举个例子：
```
let input = [1, 2]
let [first, second] = input;
console.log(first) // 输出 1
console.log(second) // 输出 2
这样就相当于创建了2个变量：first和second
等同于：
let first = input[0] = 1
let second = input[1] = 2
```
**解构作用域已声明的变量会更好**很方便操作数据
举个例子：（互换）
```
[first, second] = [second, first]
就相当于，把[1,2] 的数组变成 [2, 1]了
```
作用于函数参数，举个例子：
```
function f([first, second]: [number, number]) {
    console.log(first);
    console.log(second);
}
f(input);
```
在数组里使用`...`语法，创建剩余变量,举个例子：
```
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4 ]
```

### 2.对象解构
什么叫对象解构？举个例子
```
let obj = {
  name: 'lucky',
  age: 18,
  height: 168
}
let {name, age} = obj
这个就相当于通过obj.name 和obj.age 创建了 name和age，如果不需要c就可以忽略它
```
....这个。。。 我后面的暂时没看懂（需要的自行看文档吧）
———————————————这是个需要补缺补漏的提醒———————————————————

最后最后，谨慎使用解构，一不小心会把自己绕进去的:joy:

## 展开
展开与解构正相反，它允许你将一个数组展开为另一个数组，将一个对象展开为另一个对象。
### 1. 展开数组
举个例子
```
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];  
这就相当于bothPlus == [0, 1, 2, 3, 4, 5]
```
展开操作创建了first和second的一份浅拷贝，它们两不会被展开的操作所影响。
### 2. 展开对象
```
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { ...defaults, food: "rich" };
这就相当于
search = {
  food: 'rich', // rich 覆盖 spicy
  price: '$$',
  ambiance: 'noisy'
}
```
可以看出来，对象的展开比数组的复杂，**展开对象后面的属性会覆盖前面的属性**
假如search == {food:"rich", ...defaults}
结果就是：
```
search = {
  food: 'spicy', // spicy覆盖rich
  price: '$$',
  ambiance: 'noisy'
}
```


——————————————————END——————————————————————————
—————————————终于结束了的分隔符——————————————————
## 参考资料
- [TypeScript官方文档](https://www.tslang.cn/docs/handbook/variable-declarations.html)
- [TypeScript英文文档](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md)
- [javascript中var、let、const声明的区别(segmentfault——fanqifeng)](https://segmentfault.com/a/1190000012221834)
- [在for循环中运行setTimeout的三种情况(CSDN——我升4级啦啦啦)](https://blog.csdn.net/Febby_/article/details/94763441)


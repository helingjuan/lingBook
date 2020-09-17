# JS基础面试题
<!-- TOC -->

- [JS基础面试题](#js基础面试题)
  - [一.js基础](#一js基础)
    - [1. 讲讲JS的数据类型？9种](#1-讲讲js的数据类型9种)
    - [2. 讲讲原型链？](#2-讲讲原型链)
    - [3. 讲讲this](#3-讲讲this)
      - [函数调用方式](#函数调用方式)
    - [4. 浅拷贝和深拷贝的区别？](#4-浅拷贝和深拷贝的区别)
    - [5. 实现一个深拷贝](#5-实现一个深拷贝)
    - [6. 讲讲事件冒泡和事件捕获以及事件代理？](#6-讲讲事件冒泡和事件捕获以及事件代理)
    - [7. 什么是闭包？](#7-什么是闭包)
      - [闭包的作用](#闭包的作用)
      - [闭包的注意点](#闭包的注意点)
      - [考察](#考察)
    - [8. null和undefined的区别？](#8-null和undefined的区别)
  - [二.ES6基础](#二es6基础)
    - [1. 讲讲Map和Set？](#1-讲讲map和set)
      - [什么是Map？](#什么是map)
      - [什么是Set？](#什么是set)
      - [数组去重的几种方法？:star::star::star::star::star:](#数组去重的几种方法️️️️️)
    - [2. WeakMap和Map之间的区别？](#2-weakmap和map之间的区别)
      - [区别](#区别)
    - [3. ES6的新特性？](#3-es6的新特性)
    - [4. const,let和var之间的区别？以及解决了什么问题](#4-constlet和var之间的区别以及解决了什么问题)
      - [var 存在的问题](#var-存在的问题)
      - [const和let的主要特性](#const和let的主要特性)
    - [5. 什么是箭头函数？](#5-什么是箭头函数)
      - [箭头函数的注意点](#箭头函数的注意点)
- [参考资料](#参考资料)

<!-- /TOC -->

## 一.js基础
### 1. 讲讲JS的数据类型？9种
  - 6种原始类型
    - Boolean
    - Number
    - String
    - Symbol
    - Undefined
    - BigInt
  - Null
  - Object
  - Function
### 2. 讲讲原型链？
原型链的主要目的，是实现继承。通过原型让一个引用类型继承另一个引用类型的实例和方法。
缺点主要有2个：
 1. 引用类型的所有属性和方法都被其实例所共享，容易污染数据
 2. 在创建子类型实例的时候，不能向超类型的构造函数中传递参数

解决方法：**借助构造函数**，在子类型构造函数的内部调用超类型的构造函数，通过call()或者apply(),这样就可以在每个子类型实例中创建一份超类型的实例副本，如果该子类型修改其超类型的数据，就不会影响到其他子类型实例。
### 3. 讲讲this
this 是js非常重要的关键词之一，表示函数的当前执行上下文
理解this的关键是要清楚的知道函数调用以及如何影响上下文
```
function doSomething() {
   this.style.color = '#cc0000';
}
```
在js中，this总是指向执行的函数或者是函数对象。当我们定义函数在页面上，这个this的指向就是这个页面或者是window对象。在点击事件，this的指向就是html元素
当我们执行函数`doSomething()`时，this就是指向window。

举个例子
```
var obj = {
  foo: function(){
    console.log(this)
  }
}

var bar = obj.foo
obj.foo() // 打印出的 this 是 obj
bar() // 打印出的 this 是 window
```
#### 函数调用方式
js里有3种函数调用形式
```
func(p1, p2) === func.call(undefined, p1,p2)
obj.child.method(p1, p2) === obj.child.method(obj.child, p1,p2)
func.call(context, p1, p2) // 先不讲 apply，这才是正常调用形式，上面两种都是语法糖，可以等价的变成call形式
```
**this就是这里的context**！
> 当context为undefined或null时，那么window对象就是默认的context，在严格模式下，context就是undefined
### 4. 浅拷贝和深拷贝的区别？
### 5. 实现一个深拷贝
### 6. 讲讲事件冒泡和事件捕获以及事件代理？
### 7. 什么是闭包？
主要是为了解决作用域问题，让外部函数可以访问内部函数的变量的函数，即**能够读取其他行数内部变量的函数**
因为在js中，只有函数内部的子函数才能读取其局部变量，所以闭包也可以理解为**定义在函数内部的函数**

#### 闭包的作用
1. 读取函数内部的变量
2. 让函数内部的变量值始终保持在内存中

举个例子：
```
function f1(){

　　　　var n=999;

　　　　nAdd=function(){n+=1}

　　　　function f2(){
　　　　　　alert(n);
　　　　}

　　　　return f2;

　　}

　　var result=f1();

　　result(); // 999

　　nAdd();

　　result(); // 1000
```

解析： 在这段代码中，result实际上就是闭包f2函数。它一共运行了两次，第一次的值是999，第二次的值是1000。这证明了，函数f1中的局部变量n一直保存在内存中，并没有在f1调用后被自动清除。

为什么会这样呢？原因就在于f1是f2的父函数，而f2被赋给了一个全局变量，这导致f2始终在内存中，而f2的存在依赖于f1，因此f1也始终在内存中，不会在调用结束后，被垃圾回收机制（garbage collection）回收。

这段代码中另一个值得注意的地方，就是"nAdd=function(){n+=1}"这一行，首先在nAdd前面没有使用var关键字，因此nAdd是一个全局变量，而不是局部变量。其次，nAdd的值是一个匿名函数（anonymous function），而这个匿名函数本身也是一个闭包，所以nAdd相当于是一个setter，可以在函数外部对函数内部的局部变量进行操作

#### 闭包的注意点
1. 因为闭包会使得函数的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题
2. 闭包会在父函数外部，改变父函数内部变量的值。

#### 考察
第一题：
```
var name = "The Window";

　　var object = {
　　　　name : "My Object",

　　　　getNameFunc : function(){
　　　　　　return function(){
　　　　　　　　return this.name;
　　　　　　};

　　　　}

　　};

　　alert(object.getNameFunc()());// The WIndow
```
??? 为什么不是`My Object`

第二题：
```
var name = "The Window";

　　var object = {
　　　　name : "My Object",

　　　　getNameFunc : function(){
　　　　　　var that = this;// 重点
　　　　　　return function(){
　　　　　　　　return that.name;
　　　　　　};

　　　　}

　　};

　　alert(object.getNameFunc()());// My Object
```
引申出来this指向的问题了。
> this关键字代表的实例会根据环境不同而变化的

### 8. null和undefined的区别？
他们两都是**所有类型的子类型**，可以把赋值给任意类型。
它们两的含义都是空，但是空的指向是不一样的。
null 是空指针对象，一般用于参数准备声明为对象，但是还没赋值时，就可以声明为null，表示这个是个对象变量；
undefined 就是变量声明但是没有赋值时，那个变量的值；

## 二.ES6基础
### 1. 讲讲Map和Set？
#### 什么是Map？
JS中**对象的本质**是，**键值对的集合**就是Hash结构，只能用**字符串作为键名**
而Map结构是对这个的升级，也是键值对的集合，但是是更完善的Hash结构，**各种类型的值都可以当做键名，包括对象**
因为键名支持多种类型，所以对键名的判断很重要

> **键名判断**
> - 简单类型（数字，字符串，布尔值）
> 这种，**值相等**即为同一个键
> - 复杂类型（对象）
> **只有对同一个对象的引用，才是同一个键**
> 键实际上是与内存地址相绑定的，只要内存地址不同，就视为两个地址

#### 什么是Set？
一种新的数据结构，类似**数组**，但是**成员的值都是唯一的，不会重复**,若添加一个已有的值，是加不成功的，因为set中已经有了。
其本身是一个构造函数，生成Set数据结构。
加入成员的方法：`add()`

> 向set加入值的时候，不会发生类型转换，比如 5和“5”就是不同的值
> Set内部判断两个值是否相等的算法是：**Same-value equality**，原理类似“===”，但是这里NaN等于自身

所以可以利用set这个特性，用来**数组去重**
方法：
- `[...new Set(array)]` 
- `Array.from(new Set(array))`
  
#### 数组去重的几种方法？:star::star::star::star::star:
1. set方法：
   - `[...new Set(array)]` 
   - `Array.from(new Set(array))`

### 2. WeakMap和Map之间的区别？
WeakMap与map类似，但有区别
#### 区别
1. WeakMap只接受对象作为键名（null除外）
2. WeakMap的键名所指向的对象不计入垃圾回收机制
   key值弱引用，对垃圾回收更加友好
3. WeakMap无遍历操作，也无Size属性
4. WeakMap不支持clear方法，只有4个方法可用：`get(),set(),has(), delete()`

### 3. ES6的新特性？

1. 变量新增 const和let
2. 有了箭头函数
3. Promise
4. 字符串模板
5. 增加多个数组方法，比如for...of循环,reduce,filter
6. 模块化Module（这个被提到了）
7. 对象和数组的解构赋值
8. 扩展运算符
9. 增加类的概念

### 4. const,let和var之间的区别？以及解决了什么问题
const和let的出现主要是解决var的存在的几个问题，比如变量提升，变量重复等问题

#### var 存在的问题

1. 变量提升
2. 变量的作用域可以是块级的和全局的
3. 变量可以重新赋值
4. 可以重复声明变量

#### const和let的主要特性

1. 变量的作用域都是块级作用域，不存在变量提升的情况
2. const类型的变量，不可以重复赋值，因为这是个常量；let可以重复赋值，这样就可以从声明上就很明确的区分开变量和常量了
3. const和let都不支持重复声明变量，如果二次声明同一个变量，会报错的，因为使用let和const声明的变量在该作用域内是唯一的


### 5. 什么是箭头函数？
就是函数的一种简写形式
最主要的特点是：
1. 不需要function关键字来创建函数
2. 只有一行的时候，可以省略return关键字
3. 继承当前上下文的this关键字

最主要的作用就是this这个了。
在箭头函数出现之前，每个函数都是根据它是被如何调用的来定义这个函数的this值
- 构造函数，this就指向一个新对象
- 严格模式下的函数调用，this指向undefined
- 如果是对象方法，则this指向这个对象
- 非严格模式下的函数调用，this指向window对象

**箭头函数不会创建自己的this，它只会从自己作用域链的上一层继承this**，因此，this是继承来的。箭头函数没有自己的this指针

#### 箭头函数的注意点
1. 无论在严格模式还是非严格模式下，箭头函数都不能具有重复的命名参数
2. 箭头函数没有arguments绑定，但是它们可以访问最接近的非箭头父函数的argument对象
3. 箭头函数永远不能用作构造函数，不存在prototype属性
4. 在函数的整个生命周期内，箭头函数内部的值保持不变，并且总是与接近的非箭头父函数中的值绑定
# 参考资料
- [学习Javascript闭包（Closure）——（blog：阮一峰）](https://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)
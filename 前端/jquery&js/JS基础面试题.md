# JS基础面试题
<!-- TOC -->

- [JS基础面试题](#js基础面试题)
  - [一.js基础](#一js基础)
    - [1. 讲讲JS的数据类型？9种](#1-讲讲js的数据类型9种)
    - [2. 讲讲原型链？](#2-讲讲原型链)
    - [3. 讲讲this](#3-讲讲this)
      - [函数调用方式](#函数调用方式)
    - [4. 浅拷贝和深拷贝的区别？](#4-浅拷贝和深拷贝的区别)
      - [什么是赋值？](#什么是赋值)
      - [什么是浅拷贝？](#什么是浅拷贝)
      - [什么是深拷贝？](#什么是深拷贝)
    - [4.2 实现一个浅拷贝](#42-实现一个浅拷贝)
      - [1. `Object.assign()`](#1-objectassign)
      - [2. `Array.prototype.concat()`](#2-arrayprototypeconcat)
      - [3. `Array.prototype.slice()`](#3-arrayprototypeslice)
    - [5. 实现一个深拷贝](#5-实现一个深拷贝)
      - [1. `JSON.parse(JSON.stringify(obj))`](#1-jsonparsejsonstringifyobj)
      - [2. 手写递归方法](#2-手写递归方法)
      - [3. 函数库`lodash`](#3-函数库lodash)
    - [6. 讲讲事件冒泡和事件捕获？](#6-讲讲事件冒泡和事件捕获)
      - [什么是事件流？](#什么是事件流)
      - [什么是事件冒泡？](#什么是事件冒泡)
      - [什么是事件捕获？](#什么是事件捕获)
      - [什么是DOM事件流？](#什么是dom事件流)
      - [一个有趣的例子:question:(害，不会)](#一个有趣的例子害不会)
    - [6.2 什么是事件委托（事件代理）？](#62-什么是事件委托事件代理)
      - [什么是事件委托？](#什么是事件委托)
      - [为什么要用事件委托？](#为什么要用事件委托)
      - [适合用事件委托的事件](#适合用事件委托的事件)
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
      - [箭头函数的作用](#箭头函数的作用)
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
浅拷贝和深拷贝都是针对引用数据类型（对象和数组）来说的
#### 什么是赋值？
当我们把一个对象赋值给一个新的变量时，**赋的其实是该对象在栈中的地址**，而不是堆中的数据。也就是**两个对象指向同一个存储空间**，修改新对象会影响原对象
#### 什么是浅拷贝？
浅拷贝是**按位拷贝对象**，会创建一个新对象，这个对象有着原始对象属性值的一份精准拷贝。如果对象是基本类型，拷贝的就是这个基本类型的值；如果是引用类型（对象属性值是内存地址），拷贝的就是这个内存地址。因此如果其中一个对象改变了这个地址，就会影响到另一个对象。即默认拷贝构造函数**只对对象进行浅拷贝**，只复制对象空间不复制资源。

浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存，修改新对象会修改到原对象
也就是说，如果对象中的属性值是多种类型的，对于基本类型复制的是值，对引用类型，复制的是内存地址。

#### 什么是深拷贝？
深拷贝会另外创建一个一模一样的对象，新旧对象不共享内存，修改新对象不会改到原对象

### 4.2 实现一个浅拷贝
有这么几种方法：
1. `Object.assign()`
2. `Array.prototype.concat()`
3. `Array.prototype.slice()`
4. ES6的扩展运算符`...`
5. `Object.create()`

#### 1. `Object.assign()`
`Object.assign()`可以把任意多个源对象自身的可枚举属性拷贝给目标对象，然后返回目标对象。
但是这个拷贝是浅拷贝，拷贝的是对象的属性的引用（内存地址），而不是对象本身。

> 注意：**当源对象只有一层时（对象的属性都是基本数据类型的），是深拷贝**

#### 2. `Array.prototype.concat()`
使用数组的concat()方法
#### 3. `Array.prototype.slice()`
就是使用数组的slice()方法

> slice()和concat()方法不修改原数组，只会返回一个浅复制了原数组中的元素的一个新数组

### 5. 实现一个深拷贝
有这么几种方法：
1. 粗暴法：`JSON.parse(JSON.stringify())`
2. 手写递归方法:star::star::star::star::star:(推荐！！！)
3. 函数库`lodash`

#### 1. `JSON.parse(JSON.stringify(obj))`
原理： 用`JSON.stringify()`会将对象转成JSON字符串，再用`JSON.parse()`把字符串解析成对象，一去一来，新的对象就产生了，而且对象会开辟新的栈，实现深拷贝。

缺点：
1. 不能处理函数
   可以实现数组或对象深拷贝，但是**不能处理函数**，因为`JSON.stringify()`是将js值（对象或数组）转换成一个JSON字符串，不接受函数。
2. 会抛弃对象的constructor
  深拷贝之后，不管这个对象原来的构造函数是什么，在深拷贝之后都会变成Object

#### 2. 手写递归方法
通过递归，实现**深度克隆原理**：遍历对象、数组直到里面都是基本数据类型，然后再去复制，就是深度拷贝
举个例子：
```
// 定义检测数据类型的功能函数！！！（这个是最核心的部分，判断数据类型）
function checkType(target) {
  return Object.prototype.toString.call(target).slice(8, -1)
}
// 深度克隆
function cloneDeep(target) {
  // 判断拷贝的数据类型
  let result, targetType = checkType(target)
  switch (targetType) {
    case 'Object':
      result = {}
      break
    case 'Array':
      result = []
      break
    default: // 基本数据类型，直接返回值即可
      return target
  }
  // 遍历目标数据
  for (let i in target) {
    let value = traget[i]
    if (checkType(value) === 'Object' || checkType(value) === 'Array') { // 如果是引用类型，则继续递归进去，取出其基本数据类型
      result[i] = cloneDeep(value) // 递归调用
    } else {
      result[i] = value // value值是基本数据类型，就直接赋值
    }
  }
  return result // 返回最后结果
}
```
#### 3. 函数库`lodash`
使用lodash的`cloneDeep(obj)`方法
举个例子：
```
var lodash = require('lodash')
var obj = {
  a: 1,
  b: {
    f: {
      g: 1
    }
  },
  c: [1, 2, 3]
}
var obj2 = lodash.cloneDeep(obj)
console.log(obj.b.f === obj2.b.f) // false
```

### 6. 讲讲事件冒泡和事件捕获？
#### 什么是事件流？
事件流描述的是从页面中接收事件的顺序。
IE事件流是**事件冒泡**；Netscape的事件流是**事件捕获**

#### 什么是事件冒泡？
就是**事件从开始时由最具体的元素接收**，然后逐级向上传播到较为不具体的节点（文档），直至到window对象
#### 什么是事件捕获？
就是不太具体的节点（window对象）应该更早地接收到事件，而**最具体的节点应该是最后接收到事件**。和事件冒泡的事件流是完全相反的。
主要作用： 在事件到达预订目标之前捕获它
> 目前因为老版本浏览器不支持，所以很少使用

#### 什么是DOM事件流？
DOM2级事件规定事件流包括3个阶段：事件捕获阶段，处于目标阶段和事件冒泡阶段。

事件流流程：
1. 首先发生**事件捕获**：
   为截获事件提供了机会
2. 实际的目标接收事件
3. 事件冒泡阶段，可以在这个阶段对事件作出响应

#### 一个有趣的例子:question:(害，不会)
```
// html
<div id="a">
    <div id="b">
        <div id="c"></div>
    </div>
</div>


// css
#a{
    width: 300px;
    height: 300px;
    background: pink;
}
#b{
    width: 200px;
    height: 200px;
    background: blue;
}
#c{
    width: 100px;
    height: 100px;
    background: yellow;
}

// js
var a = document.getElementById("a"),
    b = document.getElementById("b"),
    c = document.getElementById("c");
c.addEventListener("click", function (event) { // c的事件冒泡
    console.log("c1");
    // 注意第三个参数没有传进 false , 因为默认传进来的是 false
    //，代表冒泡阶段调用，个人认为处于目标阶段也会调用的
});
c.addEventListener("click", function (event) { // c的事件捕获
    console.log("c2");
}, true);
b.addEventListener("click", function (event) { // b的事件捕获
    console.log("b");
}, true);
a.addEventListener("click", function (event) { // a的事件捕获1
    console.log("a1");
}, true);
a.addEventListener("click", function (event) { // a的事件冒泡
    console.log("a2")
});
a.addEventListener("click", function (event) { // a的事件捕获2
    console.log("a3");
    event.stopImmediatePropagation();
}, true);
a.addEventListener("click", function (event) { // a的事件捕获3
    console.log("a4");
}, true);
```
有3个问题：
1. 如果点击c或者b，输出什么？
2. 如果点击a，输出什么？
3. 如果注释掉`event.stopImmediatePropagation`,点击c，会输出什么？

分析：
1. **如果点击c或者b，输出什么？**
`a1,a3`
解析：按DOM事件流处理，先进行事件捕获，然后再目标事件，然后再事件冒泡。所以先判断a的事件捕获即a1，a3,a4,因为a3中的`stopImmediatePropagation`包含了`stopPropagation`功能，阻止事件传播（捕获或冒泡），但同时也阻止该元素上后来绑定的事件处理程序被调用，所以不输出a4。因为事件捕获被拦截了，自然不会触发b，c上的事件，所以不输出b，c1,c2,冒泡更谈不上了，所以不输出a2.

2. **如果点击a，输出什么？**
`a1,a2,a3`
解析：现在事件流是处于目标阶段，不是冒泡阶段、也不是捕获阶段，事件处理程序被调用的顺序是**注册的顺序**。不论你指定的是true还是false。换句话来说就是现在点击的是a这个盒子本身，它处于事件流的目标状态，而既非冒泡，又非捕获。（需要注意的是，此时的eventPhase为2，说明事件流处于目标阶段。当点击a的时候，先从document捕获，然后一步步往下找，找到a这个元素的时候，此时的target和currentTarget是一致的，所以认定到底了，不需要再捕获了，此时就按顺序执行已经预定的事件处理函数，执行完毕后再继续往上冒泡...）

3. **如果注释掉`event.stopImmediatePropagation`,点击c，会输出什么？**
我的答案：`a1, a3, a4, b, c2, c1, a2` X
实际的答案：`a1, a3, a4, b, c1, c2, a2`√
解析：如果同一个事件处理程序（指针相同，比如用 handler 保存的事件处理程序），用 addEventListener或 attachEvent绑定多次，如果第三个参数是相同的话，也只会被调用一次。当然，如果第三个参数一个设置为true，另一个设置为false，那么会被调用两次。
而在这里，都是给监听函数的回调赋予了一个匿名函数，所以其实每个处理函数都会被调用。需要注意的是，如果你还不明白为什么在c上触发的先是c1再是c2的话，那么你就需要在去看看第二个问题所描述的内容了。

### 6.2 什么是事件委托（事件代理）？
事件代理就是基于事件冒泡原理，在父元素做事件的处理，可以实现减少dom操作次数和降低内存使用（不用给每个元素都添加同样的函数）
#### 什么是事件委托？
事件委托就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。即**委托父级代为执行事件**。

> 具体例子：取快递
> 有三个同事预计会在周一收到快递。为签收快递，有两种办法：一是三个人在公司门口等快递；二是委托给前台MM代为签收。现实当中，我们大都采用委托的方案（公司也不会容忍那么多员工站在门口就为了等快递）。前台MM收到快递后，她会判断收件人是谁，然后按照收件人的要求签收，甚至代为付款。这种方案还有一个优势，那就是即使公司里来了新员工（不管多少），前台MM也会在收到寄给新员工的快递后核实并代为签收。
> 
>这里其实还有2层意思的：
第一，现在委托前台的同事是可以代为签收的，即程序中的现有的dom节点是有事件的；
第二，新员工也是可以被前台MM代为签收的，即程序中新添加的dom节点也是有事件的。

#### 为什么要用事件委托？
假如我们有100个li，每个li都有相同的click点击事件，可能我们会用for循环的方法，来遍历所有的li，然后给它们添加事件，那这么做会存在什么影响呢？

在JavaScript中，**添加到页面上的事件处理程序数量将直接关系到页面的整体运行性能**，因为需要不断的与dom节点进行交互，**访问dom的次数越多，引起浏览器重绘与重排的次数也就越多**，就会延长整个页面的交互就绪时间，这就是为什么性能优化的主要思想之一就是减少DOM操作的原因；如果要**用事件委托，就会将所有的操作放到js程序里面，与dom的操作就只需要交互一次**，这样就能大大的减少与dom的交互次数，提高性能；

**每个函数都是一个对象，是对象就会占用内存，对象越多，内存占用率就越大**，自然性能就越差了（内存不够用，是硬伤，哈哈），比如上面的100个li，就要占用100个内存空间，如果是1000个，10000个呢，那只能说呵呵了，如果用事件委托，那么我们就可以只对它的父级（如果只有一个父级）这一个对象进行操作，这样我们就需要一个内存空间就够了，是不是省了很多，自然性能就会更好。
#### 适合用事件委托的事件
`click, mousedown,mouseup, keydown, keyup, keypress`

> 虽然`mouseover和mouseout`也有事件冒泡，但是处理它们的时候需要特别注意，因为需要经常计算它们的位置，处理起来较麻烦

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

#### 箭头函数的作用
1. 简短且不绑定this

# 参考资料
- [学习Javascript闭包（Closure）——（blog：阮一峰）](https://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)
- [浅拷贝与深拷贝的区别——（segmentfault：coding小姐姐）](https://segmentfault.com/a/1190000018874254)
- [你真的理解事件冒泡和事件捕获吗？——(segmentfault：绪北)](https://segmentfault.com/a/1190000012729080)
- [js中的事件委托或是事件代理详解——（博客园：凌云之翼）](https://www.cnblogs.com/liugang-vip/p/5616484.html)
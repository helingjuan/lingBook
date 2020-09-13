# js 原型和原型链了解一下
<!-- TOC -->

- [js 原型和原型链了解一下](#js-原型和原型链了解一下)
  - [什么是原型？`prototype`](#什么是原型prototype)
  - [什么是原型链？`__proto__`](#什么是原型链__proto__)
    - [原型链的作用](#原型链的作用)
    - [原型链存在的问题](#原型链存在的问题)
  - [原型指向构造函数的方法 `constructor`](#原型指向构造函数的方法-constructor)
  - [实例与原型](#实例与原型)
    - [如何确认原型和实例的关系？](#如何确认原型和实例的关系)
    - [Q：原型的原型是什么？](#q原型的原型是什么)
  - [关于`Function.__proto__ === Function.prototype`分析](#关于function__proto__--functionprototype分析)
  - [总结](#总结)
    - [prototype 和`__proto__`的区别](#prototype-和__proto__的区别)
- [参考资料](#参考资料)

<!-- /TOC -->

## 什么是原型？`prototype`
**prototype是每个函数都会有的属性，而这个属性就指向这个函数的原型。**

举个例子：
```
function Person() {

}
// 虽然写在注释里，但是你要注意：
// prototype是函数才会有的属性
Person.prototype.name = 'Kevin';// 在原型上定义name参数，且name = 'Kevin'
var person1 = new Person();
var person2 = new Person();
console.log(person1.name) // Kevin
console.log(person2.name) // Kevin
```

> 每一个JavaScript对象(null除外)在**创建**的时候就会与之关联另一个对象，这个对象就是我们所说的原型，**每一个对象都会从原型"继承"属性**

**可以用`Object.prototype`表示该实例所指向的原型**
> 所有引用类型默认都继承了Object，也就是说所有函数的默认原型都是Object的实例。
## 什么是原型链？`__proto__`
每一个JavaScript对象（实例）（null除外）都具有的一个属性，叫`__proto__`,这个属性指向该对象的原型

举个例子：
```
function Person() {

}
var person = new Person();
console.log(person.__proto__ === Person.prototype); // true

```
实例对象的`__proto__`和构造函数的prototype均指向原型
### 原型链的作用
这是js实现继承的主要方法，利用原型让一个引用类型继承另一个引用类型的属性和方法
### 原型链存在的问题
1. 包含引用类型值的原型属性会被所有实例共享，也就是在某个实例中修改原型中的属性值时，所有实例的属性值都被修改了，容易污染数据
2. 在创建子类型的实例时，不能像超类型的构造函数传递参数

解决方法：**借用构造函数**，就是在子类型的构造函数的内容部调用超类型的构造函数，这样会在每个子类型的实例的环境下调用超类型的构造函数，这样，每个实例都会具有自己的原型副本了。
举个例子：
```
function SuperType () {
  this.colors = ['red', 'blue', 'green']
}
function SubType() {
  // 继承SuperType,调用了SubType的构造函数
  SuperType.call(this)
}
var instance1 = new SubType()
instance1.colors.push('black') // colors = 'red', 'blue', 'green', 'black
var instance2 = new SUbType()
instance2.colors // 'red', 'blue', 'green'
```
## 原型指向构造函数的方法 `constructor`
每个原型都有一个constructor属性指向其关联的构造函数
举个例子：
```
function Person() {

}
console.log(Person === Person.prototype.constructor); // true
// Person是构造函数
// Person.prototype 指向Person的原型
// Person.prototype.constructor 指向Person原型的构造函数，而Person就是其构造函数，就是指向其本身
```
## 实例与原型
当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还找不到，就去找原型的原型，一直找到最顶层（NULL）为止
举个例子：
```
function Person() {

}

Person.prototype.name = 'Kevin'; // 给Person的原型增加/编辑 name = 'Kevin'

var person = new Person(); // person 是Person的实例

person.name = 'Daisy'; // person增加name属性，属性值为'Daisy'
console.log(person.name) // Daisy

delete person.name; // 删除name属性，
console.log(person.name) // Kevin Person构造函数中就没有name属性，就往原型上查找，如果原型上也没有，那就去原型的原型，
```
### 如何确认原型和实例的关系？
有两种方法：
1. `instanceof`操作符，测试实例与原型链中出现过的构造函数
2. `isPrototypeOf()` 
  
> 只要是原型链中出现过的原型，都可以说是该原型链所派生的实例的原型
### Q：原型的原型是什么？
因为原型也是一个**对象**，也就是说，原型对象是通过Object构造函数生成的，所以原型的原型就是指**Object**构造函数。
那Objec的原型是谁？
众所周知，万物皆空，**Object的原型是Null**，
Null的实质其实是一个**空对象指针**，所以就有这么一条规则：**只要意在保存对象的变量，还没真正保存对象，最好将该变量初始化为null**
举个例子：
```
// Object的原型 Object.prototype 就是指向Object的原型的实例 即Null
// NUll的实例的`__proto__`就是指向其构造函数NULL 空指针
console.log(Object.prototype.__proto__ === null) // true
```
所以一般查到Object.prototype时，就可以停止查找了。
## 关于`Function.__proto__ === Function.prototype`分析
```
/ 这是底层实现的
const protoObj = Function.prototype;
Function.__proto__ = protoObj;
// 也就是说
// Function.prototype --> addressA
// Function.__proto__ --> addressA
```
因为**Function在任何引擎执行代码之前已经在内存中了**，只不过一个对象的标识符的两个属性应用了同一个地址而已。
之所以这么设置，是因为要保持一致性，Function自身就是一个函数。

## 总结
构造函数的`prototype`属性指向原型，原型链通过`__proto__`链接起来
原型链的本质：就是创建父类型构造函数的实例，并将该实例赋给子类型的prototype属性，所以可以从子类型实例的`__proto__`追溯其继承的原型链
就是：
```
const instance = new Person()
原型链查找流程：
1. instance.__proto__ // 查询实例的原型，就是Person构造函数，所以就从Person构造函数继续往上查，又构造函数都有prototype属性
2. Person.prototype // 查询构造函数Person的原型，就是Object构造函数的实例，即const obj = new Object,即obj，找到Object的实例，又实例都有__proto__属性，继续查找实例的原型
3. obj.__proto__ // 查找obj实例的原型，就是Object构造函数的原型，即Null的实例，就是null
```
### prototype 和`__proto__`的区别
prototype是函数才有的属性，而`__proto__`是所有对象（实例）都有的属性

# 参考资料
- [JavaScript深入之从原型到原型链——(Github：mqyqingfeng)](https://github.com/mqyqingfeng/Blog/issues/2)
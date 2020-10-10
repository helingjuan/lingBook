---
title: TypeScript学习二：基础类型
tags: typescript
notebook: 前端
---
[]
# TypeScript学习二：基础类型
目录：
- [TypeScript学习二：基础类型](#typescript%E5%AD%A6%E4%B9%A0%E4%BA%8C%EF%BC%9A%E5%9F%BA%E7%A1%80%E7%B1%BB%E5%9E%8B)
    - [*.变量声明 `let`](#%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E-let)
    - [1.布尔值 `boolean`](#1%E5%B8%83%E5%B0%94%E5%80%BC-boolean)
    - [2.数字 `number`](#2%E6%95%B0%E5%AD%97-number)
    - [3.字符串 `string`](#3%E5%AD%97%E7%AC%A6%E4%B8%B2-string)
    - [4.数组 `Array`](#4%E6%95%B0%E7%BB%84-array)
      - [4.1 直接在元素类型后面加[]](#41-%E7%9B%B4%E6%8E%A5%E5%9C%A8%E5%85%83%E7%B4%A0%E7%B1%BB%E5%9E%8B%E5%90%8E%E9%9D%A2%E5%8A%A0)
      - [4.2 使用数组泛型声明 Array<元素类型>](#42-%E4%BD%BF%E7%94%A8%E6%95%B0%E7%BB%84%E6%B3%9B%E5%9E%8B%E5%A3%B0%E6%98%8E-array%E5%85%83%E7%B4%A0%E7%B1%BB%E5%9E%8B)
    - [5.对象 `Object`](#5%E5%AF%B9%E8%B1%A1-object)
    - [6.元组 `Tuple`](#6%E5%85%83%E7%BB%84-tuple)
    - [7.枚举 `enum`](#7%E6%9E%9A%E4%B8%BE-enum)
    - [8.任意 `any`](#8%E4%BB%BB%E6%84%8F-any)
    - [9.void](#9void)
    - [10.null和undefined](#10null%E5%92%8Cundefined)
    - [11.never](#11never)
    - [12.类型断言](#12%E7%B1%BB%E5%9E%8B%E6%96%AD%E8%A8%80)
    - [参考资料](#%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)


typescript支持与JavaScript几乎相同的数据类型。大概有这几种：  
- 布尔值 `boolean`
- 数字 `number`
- 字符串 `string`
- 数组 `Array`
- 对象 `Object`
- 元组 `Tuple`
- 枚举 `enum`
- 任意 `any`
- void
- null
- undefined
- never
- 类型断言

### *.变量声明 `let`
JavaScript一般都是用var来声明变量，且不用具体指定变量所属的变量类型，变量类型会根据变量的值来确定。
且var 声明的变量是全局的，这样就会造成数据污染等等问题。
TypeScript里优化了这一点，用let代替var，解决了很多var的痛点。
### 1.布尔值 `boolean`
值只有2种，true 或者 false。一般用于某种条件判断
```
let isSelect: boolean = false;
```

### 2.数字 `number`
和javaScript一样，TypeScript里的**数字都是浮点数**，支持十进制、十六进制、二进制和八进制。
```
let decLiteral: number = 6; // 十进制
let hexLiteral: number = 0xf00d; // 十六进制
let binaryLiteral: number = 0b1010; // 二进制
let octalLiteral: number = 0o744; // 八进制
```
其中，二进制和八进制是根据ES2015的规则来的。
- 二进制
  以`0b或者0B`开头
- 八进制
  以`0o或者0O`开头
  这个稍微注意一下，在ES2015之前，八进制是以`0`开头的，现在已经不允许了，都是以`0o或者0O`开头。
- 十六进制
  这个就不用具体介绍了，就是以`0x或者0X`开头的。

### 3.字符串 `string`
就是文本数据类型，用`""或者''`表示字符串
```
let name: string = 'LiLi'
```
还有一种更灵活的字符串形式：**模版字符串**
这种字符串就是被反引号(`)包围，并且以`${expr}`这种形式嵌入表达式。
```
let name: string = `LiLi`
let age: number = 15
let sentence: string = `Hello, ${ name}. your age will be ${ age + 1 } after next month.`
// 效果：Hello, LiLi. your age will be 16 after next month.
```

### 4.数组 `Array`
和javaScript一样。
2种声明方式：  
1. 直接在元素类型后面加[]
2. 使用数组泛型声明 Array<元素类型>

#### 4.1 直接在元素类型后面加[]
```
let arrayTemp: number[] = [1, 2, 3]
let arrayStrTemp: string[] = ['a', 'r', 'r']
```
#### 4.2 使用数组泛型声明 Array<元素类型>
```
let arrayTemp: Array<number> = [1, 2, 3]
let arrayStrTemp: Array<string> = ['a', 'r', 'r']
```

### 5.对象 `Object`
表示非原始类型，就是除了number，string，boolean，symbol，null 和undefined之外的类型。
举个例子：
```
let student: Object = {
  name: 'lucky', 
  age: 18,
  mathScore: [89, 99, 70]
  }
```
### 6.元组 `Tuple`
元祖类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。(本质还是数组吧)
```
let x: [string, number] //声明元祖类型x
x = ['lucky', 1] // 初始化x，格式要和声明的一一对应，否则会报错
```
使用场景？？？具体的我也不知道
**使用注意点：**
- 访问一个已知索引的元素，会根据元素的类型来判断这个操作是否合理。
  ```
  console.log(x[0].substr(1)) 
  console.log(x[1].substr(1))
  ```
- 访问一个越界的元素，会使用联合类型(被声明的类型中的任意一个)替代
  ```
  x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型
  console.log(x[5].toString()); // OK, 'string' 和 'number' 都有 toString
  x[6] = true; // Error, 布尔不是(string | number)类型
  ```
### 7.枚举 `enum`
这是对JavaScript标准数据类型的一个补充。枚举类型适合声明固定值的变量(常量)，比如PI=3.1415926 
当一个变量有几种可能的取值时，就可以将它定义为枚举类型。
```
enum Color {Red, Green, Blue} // 默认情况下，从0开始为元素编号，就是Color.red == 0; Color.Green == 1
let c: Color = Color.Green // 变量c是Color类型，值等于 Color.Green
```
这里有3种声明方式：
```
// 方法1：默认，从0开始为元素编号，就是Color.red == 0; Color.Green == 1
enum Color {Red, Green, Blue}
// 方法2：给定一个起始值，就是Color.red == 1; Color.Green == 2
enum Color {Red = 1, Green, Blue} 
// 方法3：全部手动赋值，就是Color.red == 2; Color.Green == 4
enum Color {Red = 2, Green = 4, Blue = 6} 
```
**注意：枚举的便利点**就是：可以由枚举的值得到这个枚举常量名。
```
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2] // colorName == 'Green'
```
### 8.任意 `any`
表示任意类型，适用于不清楚类型的一个变量。用any声明，类型检查器就不对这些值进行检查，直接通过编译阶段的检查。
**any类型允许你在编译是可选择地包含/移除类型检查。**这个和Object还是有点不一样的。Object类型的变量只是允许你给它赋任意值，但是不能够在它上面调用任意方法，即便它真的有这些方法。
举个例子：
```
let notSure: any = 4;
notSure.ifItExists(); // okay, ifItExists might exist at runtime
notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
```
### 9.void
表示没有任何类型。与any类型恰恰相反。   
一般void都是用来**声明没有返回值的函数**的。
```
function getUserName(): void {
  alert('我没有返回值')
}
```
### 10.null和undefined
他们两都是**所有类型的子类型**，可以把赋值给任意类型。
一般来说，一个变量只声明没赋值，那么它的值就是undefined
注意一点：**在指定`--strictNullChecks`标记后，null和undefined只能赋值给void和它们各自**，这样就可以避免很多常见问题。

### 11.never
表示永不存在的值的类型。never类型也是任何类型的子类型，可以赋值给任意类型，但是！**never没有子类型**，就是任何类型都不能赋值给never(除了它自己本身之外)
使用场景：
- 适用于那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型；
- 表示被永不为真的类型保护所约束的变量

举个例子：
```
// 情景1：出现死循环
function error(message: string): never {
  throw new Error(message)
}
// 情景2：也是出现死循环
function fail() {
  return error('任务失败！')
}
```
### 12.类型断言
适用于你确切知道这个变量的返回类型，就是手动指定一个值的变量。然后通过类型断言的方式告诉编译器。这样就不会进行特殊的数据检查和结构。
注意！！！**这个是只在编译阶段起作用的**。而强制类型转换是在编译和运行都起作用的。
有2种形式,效果一样(但是如果在TypeScript里使用**JSX**时，只有as语法可以使用)
```
// 方法1：尖括号语法
let someValue: any = '这是个字符串'
let strLength: number = (<string>someValue).length; //??? 有加这个尖括号的必要吗？？？难道会有强制类型转换？

// 方法2：as语法
let someValue: any = '这也是个字符串'
let strLength: number = (someValue as string).length
```
使用场景：
这个常常和**联合类型**配合使用
举个例子：
```
// level 1. 只使用联合类型
function getValue(score: string | number) {
  console.log(score.length) // 报错！因为number类型是没有length属性的
}
```
但是有时候，我们还就是不确定这个变量到底是哪个类型,那我们就得判断了
```
// level 2. 改造
function getValue(score: string | number) {
  if(score.length) { // 如果报错 就是 score.length == false
    console.log(score.length) // number类型
  } else {
    console.log(score.toString().length) // 字符串类型
  }
}
```
这时候，其实还有更方便的方法，来看！
```
// level 3. 类型断言,把score断言成number类型
// 错误例子：这个是我认为的方法，已经不需要判断了啊。。。（还未测试过）
function getValue(score: string | number) {
    console.log((<number>score).length) 
}
敲重点！！！这就是易错点，也就是我上面提醒过的。类型断言在运行时不起作用，所以并不能和强制类型转换等同。
所以如果去掉判断的话，就会出现，编译时正常，但是运行报错的情况
// 正确例子：这是网上的案例
function getValue(score: string | number) :number {
    if ((<string>score).length {
        return (<string>score).length
    }else{
        return score.toString().length;
}
}
```
**注意：类型断言不是类型转换，断言成一个联合类型中不存在的类是不可以的**
举个例子：
```
function toBoolean(something: string | number): boolean {
    return <boolean>something;// string只有string 和number类型
}

// index.ts(2,10): error TS2352: Type 'string | number' cannot be converted to type 'boolean'.
//   Type 'number' is not comparable to type 'boolean'.
```

### 参考资料
- [TypeScript官方文档](https://www.tslang.cn/docs/handbook/typescript-in-5-minutes.html)
- [TypeScript英文文档](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md)





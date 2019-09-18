---
title: TypeScript学习二：基础类型
tags: typescript
notebook: 前端
---
# TypeScript学习二：基础类型
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
### 6.元组 `Tuple`
### 7.枚举 `enum`
### 8.任意 `any`
### 9.void
### 10.null
### 11.undefined
### 12.never
### 13.类型断言


---
title: TypeScript学习一：起步
tags: typescript
notebook: 前端
---
# TypeScript学习一：起步
### 一.基基基础内容
typescript是javascript的超集，可以编译成纯JavaScript,可以在任何浏览器，任何计算机和任何操作系统上运行。且，这是一个开源项目。
#### 1.1 安装
```
npm install -g typescript
```
#### 1.2 文件拓展名 .ts
```
tsc hello.ts //编译运行hello.ts文件
```
#### 1.3 类型注解
一种轻量级的为函数或变量添加约束的方式。
```
function greeter(person: string) {
    return "Hello, " + person;
}

let user = [0, 1, 2];

document.body.innerHTML = greeter(user);
// 编译后会报错，greeter.ts(7,26): error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'. 行数要求的是string，但是我传的参数是数组，不符合规范。
```
#### 1.4 接口
```
interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Jane", lastName: "User" };

document.body.innerHTML = greeter(user);
//输出：Hello,Jane User
```
#### 1.5 类
typescript支持基于类的面向对象编程。
*注意：*  
- 类和接口可以一起共作。
- 在构造函数的参数上使用`public`等同于创建了同名的成员变量。
```
class Student {
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person : Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = new Student("Jane", "M.", "User");

document.body.innerHTML = greeter(user);
```
### 参考资料
- [TypeScript官方文档](https://www.tslang.cn/docs/handbook/typescript-in-5-minutes.html)
- [TypeScript英文文档](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md)

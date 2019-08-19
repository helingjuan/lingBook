---
title: Eslint和Tslint的区别&哪个更适合TypeScript
tags: 
notebook: 
---
# Eslint和Tslint的区别&哪个更适合TypeScript

### ESLint
——ESLint 是在 ECMAScript/JavaScript 代码中识别和报告模式匹配的工具，它的目标是保证代码的一致性和避免错误。
由Nicholas C.Zakas 创建的开源项目，目标是提供一个插件化的**javascript代码检测工具**
> 代码检查（检测）是一种静态的分析，常用与寻找有问题的模式或者代码，并且不依赖于具体的编码风格。
大多数的编程语言都有代码检查，一般来说编译程序会内置检查工具。JavaScript是一个动态的弱类型语言，在开发中比较容易出错，没有编译程序。所以就需要ESLint，在编码的过程中及时发现问题。
——ESLint官网介绍
默认情况下，ESLint支持ECMAScript5语法，当然也可以自己覆盖默认设置，启用对ECMAScript其他版本的支持。

### TSLint
——目前已经停止维护了。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190817110553.png)
### 怎么用？哪个更适合TypeScript？
- [AlloyTeam ESLint规则——github](https://github.com/AlloyTeam/eslint-config-alloy)
- 注意：ESLint团队宣布：`typescript-eslint-parser` 项目已经不再维护了。用这个插件的人，需要转而使用`@typescript-eslint/parser`
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190817113527.png)    
### 总结
**要搭配TypeScript的话，就用ESLint**，然后安装`@typescript-eslint/parser`这个插件，就可以了。
至于要怎么使用这个插件，可以看[typescript ESLint Parser官方文档(github——TypeScript ESLint)](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/parser)    
*注意*：一般来说`@typescript-eslint/parser`会和`@typescript-eslint/eslint-plugin`搭配使用。
支持的TypeScript版本范围X：`3.2.1<= X < 3.6.0`
### 参考资料
- [ESLint中文版官网](https://cn.eslint.org)
- [ESLint 在中大型团队的应用实践——美团技术团队](https://tech.meituan.com/2019/08/01/eslint-application-practice-in-medium-and-large-teams.html)
- [The futuer of TypeScript on ESLint(ESLint英文版官网)](https://eslint.org/blog/2019/01/future-typescript-eslint#the-future-of-typescript-on-eslint)
- [在Typescript项目中，如何优雅的使用ESLint和Prettier(github——forthealllight)](https://github.com/forthealllight/blog/issues/45)
- [typescript-eslint官方文档(github——TypeScript ESLint)](https://github.com/typescript-eslint/typescript-eslint)
- [typescript ESLint Parser官方文档(github——TypeScript ESLint)](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/parser)
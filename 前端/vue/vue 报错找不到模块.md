# vue 报错找不到模块
<!-- TOC -->

- [vue 报错找不到模块](#vue-%e6%8a%a5%e9%94%99%e6%89%be%e4%b8%8d%e5%88%b0%e6%a8%a1%e5%9d%97)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [Cannot find module '@/assets/img/gym-none.png'.](#cannot-find-module-assetsimggym-nonepng)
    - [原因分析](#%e5%8e%9f%e5%9b%a0%e5%88%86%e6%9e%90)
    - [解决办法](#%e8%a7%a3%e5%86%b3%e5%8a%9e%e6%b3%95)

<!-- /TOC -->
## 概述
环境：vue cli3 + vue + typescript
## Cannot find module '@/assets/img/gym-none.png'.
### 原因分析
Typescript只能识别`.ts` 和`.js`的问句，不知道怎么处理`.png`文件，所以需要让它知道该怎么处理`.png`文件
就是去加一个配置,
### 解决办法
在src根目录下找到`shims-vue.d.ts`文件(这是用脚手架创建项目，自己生成的),然后加入一句话`declare module '*.png'`

完整效果：
```
declare module '*.vue' {
  import Vue from 'vue'
  export default Vue
}

declare module '*.png'
```

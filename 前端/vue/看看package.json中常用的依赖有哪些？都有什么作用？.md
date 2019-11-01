---
title: 看看package.json中常用的依赖有哪些？都有什么作用？
tags: vue
notebook: vue 
---
# 看看package.json中常用的依赖有哪些？都有什么作用？

### 专业版的配置
```
// 完整的package.json
{
  "name": "vue-typescript-admin-template",
  "version": "0.1.0",
  "private": true,
  "author": "YS",
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint",
    "svg": "vsvg -s ./src/icons/svg -t ./src/icons/components --ext ts --es6",//生成svg 规则：-s： svg源文件， -t 图标组件生成路径，使用的依赖 vue-svgicon
    "test:e2e": "vue-cli-service test:e2e",
    "test:unit": "vue-cli-service test:unit"
  },
  "dependencies": {
    "area-data": "^5.0.6",
    "axios": "^0.19.0",
    "element-ui": "^2.10.1", //elementUI框架
    "js-cookie": "^2.2.0",
    "normalize.css": "^8.0.1",
    "nprogress": "^0.2.0",
    "path-to-regexp": "^3.0.0",
    "qs": "^6.7.0",
    "register-service-worker": "^1.6.2",
    "vue": "^2.6.10",
    "vue-area-linkage": "^5.1.0",
    "vue-class-component": "^7.1.0",
    "vue-property-decorator": "^8.2.1",
    "vue-router": "^3.1.3", // vue路由
    "vue-svgicon": "^3.2.6", //使用svg
    "vuex": "^3.1.1",
    "vuex-class": "^0.3.2",
    "vuex-module-decorators": "^0.9.9"
  },
  "devDependencies": {
    "@types/jest": "^24.0.15",
    "@types/js-cookie": "^2.2.2",
    "@types/nprogress": "^0.2.0",
    "@types/qs": "^6.5.3",
    "@types/webpack-env": "^1.14.0",
    "@typescript-eslint/parser": "^2.0.0",
    "@vue/cli-plugin-babel": "^3.9.2",
    "@vue/cli-plugin-e2e-cypress": "^3.9.0",
    "@vue/cli-plugin-eslint": "^3.9.2",
    "@vue/cli-plugin-pwa": "^3.9.0",
    "@vue/cli-plugin-typescript": "^3.9.0",
    "@vue/cli-plugin-unit-jest": "^3.9.0",
    "@vue/cli-service": "^3.9.2",
    "@vue/eslint-config-standard": "^4.0.0",
    "@vue/eslint-config-typescript": "^4.0.0",
    "@vue/test-utils": "^1.0.0-beta.29",
    "babel-core": "^7.0.0-bridge.0", // babel编译
    "babel-eslint": "^10.0.2",
    "eslint": "^6.0.1", // 代码检测和格式化
    "eslint-plugin-vue": "^5.2.3",
    "fibers": "^4.0.1",
    "jest": "^24.8.0",// 单元测试解决方案
    "sass": "^1.22.5", // css预处理器语言
    "sass-loader": "^7.1.0",
    "style-resources-loader": "^1.2.1",
    "ts-jest": "^24.0.2", 
    "typescript": "3.5.3", // 使用typescript
    "vue-cli-plugin-element": "^1.0.1",
    "vue-cli-plugin-style-resources-loader": "^0.1.3",
    "vue-template-compiler": "^2.6.10",
    "webpack": "^4.35.3"
  }
}

```
大概知道这个结构了吧，估计你现在和我刚开始的一样，一脸懵逼。那我们就来一步步解析。看看它到底配置了什么东西！
### 1.来先看下脚本部分script
```
"scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint",
    "svg": "vsvg -s ./src/icons/svg -t ./src/icons/components --ext ts --es6",
    "test:e2e": "vue-cli-service test:e2e",
    "test:unit": "vue-cli-service test:unit"
},
```
其中，`serve,build,lint`用的是同一个工具——vue-cli脚手架
- `vue-cli-service serve`就是运行项目，对应的命令`npm run serve`
- `vue-cli-service build`
- `vue-cli-service lint` 格式化，对应的命令`npm run lint`
- `vsvg -s ./src/icons/svg -t ./src/icons/components --ext ts --es6`作用：生成svg 
  - 规则：-s： svg源文件， -t 图标组件生成路径，使用的依赖 vue-svgicon
- `vue-cli-service test:e2e` 用户界面测试
- `test:unit": "vue-cli-service test:unit` 单元测试

这里重点介绍 vue-cli这个脚手架。
先思考一下：**什么是脚手架？为什么叫它脚手架？**
看看百度的解释：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191101162140.png)
所以vue-cli的作用也就显而易见了，就是用来构建前端vue项目的一个工具。
脚手架的出现就是为了减少重复性工作而引入的命令行工具。
目前流行的前端脚手架大多数都是基于nodejs编写，比如vue-cli，create-react-app等。其功能都是生成一个通用的目录结构，并配上构建、编译、检查等工程环境。
大致流程是这样的：
1. 解析用户输入的命令
2. 生成一些配置文件，比如package.json，webpack.config.js等
3. 根据用户的输入生成对应的模版项目
4. 安装该模版所需要的环境
等初始化完成后，就可以开始开发了。不用再像以前一样，为了环境头大。

### 参考资料
- [前端脚手架，听起来玄乎，实际呢？(segmentfault——Denzel)](https://segmentfault.com/a/1190000016915868)
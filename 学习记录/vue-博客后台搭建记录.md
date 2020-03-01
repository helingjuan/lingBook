# vue 博客后台搭建记录
<!-- TOC -->

- [vue 博客后台搭建记录](#vue-%e5%8d%9a%e5%ae%a2%e5%90%8e%e5%8f%b0%e6%90%ad%e5%bb%ba%e8%ae%b0%e5%bd%95)
  - [概述](#%e6%a6%82%e8%bf%b0)
    - [所需要的功能](#%e6%89%80%e9%9c%80%e8%a6%81%e7%9a%84%e5%8a%9f%e8%83%bd)
    - [用到的依赖](#%e7%94%a8%e5%88%b0%e7%9a%84%e4%be%9d%e8%b5%96)
  - [搭建开始](#%e6%90%ad%e5%bb%ba%e5%bc%80%e5%a7%8b)
    - [1.用脚手架创建项目](#1%e7%94%a8%e8%84%9a%e6%89%8b%e6%9e%b6%e5%88%9b%e5%bb%ba%e9%a1%b9%e7%9b%ae)
    - [2. 安装一些需要的依赖](#2-%e5%ae%89%e8%a3%85%e4%b8%80%e4%ba%9b%e9%9c%80%e8%a6%81%e7%9a%84%e4%be%9d%e8%b5%96)
      - [2.1 安装element-ui、babel-plugin-component、](#21-%e5%ae%89%e8%a3%85element-uibabel-plugin-component)
    - [2.2 安装axios](#22-%e5%ae%89%e8%a3%85axios)
    - [2.3 安装markdown相关的](#23-%e5%ae%89%e8%a3%85markdown%e7%9b%b8%e5%85%b3%e7%9a%84)
  - [参考资料](#%e5%8f%82%e8%80%83%e8%b5%84%e6%96%99)

<!-- /TOC -->
## 概述

就是大概所需要的的东西清单

### 所需要的功能

* [ ] 登录
* [ ] 注册
* [ ] 标签
* [ ] 关于
* [ ] 点赞和评论，还有浏览量
* [ ] 留言
* [ ] github授权登录
* [ ] 文章列表
* [ ] 文章归档
* [ ] 文章详情（支持代码语法高亮）
* [ ] 移动端适配

### 用到的依赖

- vue
- typescript
- element-ui 
  UI组件库
- webpack
- axios
- redux
- highlight.js
- marked
- vuex 
  统一状态管理
- vue-router 
  路由
- vue-class-component
  对vue组件进行了一层封装，让vue组件语法再结合了typescript语法之后更加扁平化
- vue-property-decorator
  在`vue-class-component`的基础上增强了更多结合Vue特性的装饰器，比如Prop,Emit,Inject,Model,Provide,Watch,Component(这是是从vue-class-component里继承来的)等
- vuex-class
  在`vue-class-component`写法中，绑定vuex

## 搭建开始

### 1.用脚手架创建项目

用的是vue cli3
### 2. 安装一些需要的依赖

#### 2.1 安装element-ui、babel-plugin-component、

```node
npm i element-ui -S
```

要按需映入，需要借助`babel-plugin-component`,所以再安装一下

```node
npm install babel-plugin-component -D
```
然后修改`babel.config.js`
```json
presets: ["@vue/app"],
  plugins: [
    [
      "component",
      {
        librayName: 'elemnet-ui',
        styleLibraryName: 'theme-chalk'
      }
    ]
  ]
```

### 2.2 安装axios 

```node
npm i axios -S
```

### 2.3 安装markdown相关的

## 参考资料

- [Vue + TypeScript + Element 搭建简洁时尚的博客网站及踩坑记](https://biaochenxuying.cn/articleDetail?article_id=5c9d8ce5f181945ddd6b0ffc)


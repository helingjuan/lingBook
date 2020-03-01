---
title: npm-快速操作指南
tags: 
notebook: 
---
# npm-快速操作指南
## 1. 版本管理
### 安装最新版 latest
```
npm install npm@latest -g
```
### 安装指定版本@，比如jquery
```
npm install jquery@2.2.4 --save
```
然后在package.json 中就可以看到
```
"jquery": "^2.2.4",
```

### 全局安装 -g
example模块会被安装到全局目录中
```
npm install example -g 
```

### 当前目录安装
example模块会被安装到当前命令行所在目录里
```
npm install example 
```

### 信息写入
安装的同时，会将模块信息写入package.json文件中。
```
npm install example --save 
npm install example --save-dev
```
#### `--save` 和`--save-dev`的区别
- `--save` 是上线后要依赖的东西 
  将依赖包名称添加到package.json中dependencies中；   
- `--save-dev` 是开发时候要依赖的东西
  将依赖包名称添加到package.json中devDependencies中；
## 2.命令后面的缩写是什么意思
### `-S` 
添加依赖到运行环境依赖库`dependencies`中
### `-D` 
添加依赖到`devDependencies` 就是开发环境依赖库里
### `-g`
全局安装
### 参考资料
- [npm 安装指定版本（按版本安装）(CSDN-雪梅零落)](https://blog.csdn.net/xuaner8786/article/details/81630445)


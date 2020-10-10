---
title: vue cli脚手架安装及使用
tags: vue
notebook: 前端
---
# vue cli脚手架安装及使用

## 概述

用来生成并初始化vue项目的工具，就是vue-cli 脚手架

## 安装

vue-cli3 的时候

``` npm
 npm install @vue/cli -g
```

这样就会安装最新版的，我现在就是4.1.1的
网上有说的这种命令，安装的是旧版的，目前已经被废弃，使用命令时会报错的，和你说建议使用`@vue/cli`的命令，这样才会安装到最新的版本

举个例子：
![报错栗子](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212150720.png)

## 查看vue-cli的版本号

``` npm
vue -V
```

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212151542.png)

## 使用
使用命令进行初始化项目
``` npm
vue create <projectName>
```
然后可以选择直接回车，用默认配置，或者是自定义的。

注意！！！
**那个上下键选择符只在npm里生效，在git的命令行是无效的**。所以在git命令行那里只能生成默认的，不能自定义配置。
**建议win10 用npm来初始化！**

举个例子：

- npm环境下的。
![npm环境](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/vue-cli-init.gif)
- git 命令行
![git命令行](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212152041.png)
(这里，我第一次就一直疯狂按上下左右键，一点效果都没有，就很懵，原来是vue-cli 3.0以上的版本问题，:joy:感谢segmentfault，让我摆脱苦海)

segmentFault那个回答里说的powerShell 我也试过了，不知道是我的环境问题还是啥，直接报错了
![powserShell](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212162016.png)
emmmm  散了散了，还是npm好使。
具体自定义配置过程我在其它地方再详细描述。

## 参考资料

- [vue-cli 3.0 无法选择配置(segmentfault)](https://segmentfault.com/q/1010000016371784)


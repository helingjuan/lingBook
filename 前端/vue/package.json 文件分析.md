---
title: package.json 文件分析
tags: vue
notebook: vue 
---
# package.json 文件分析
### 一.概述
基于nodejs的项目，一般其根目录下都有package.json文件。这个文件主要定义了项目的配置信息，比如名称，版本，许可证等数据。
`npm install` 就是根据package.json文件，自动下载所需要的依赖。就是配置运行项目所需要的运行和开发环境。
**注意：**
- package.json文件就是一个JSON对象，该对象的每一个成员就是当前项目的一项设置。
- 版本一般遵循`大版本.次要版本.小版本`的格式来，比如`1.0.0`


先看看一个较完整的package.json 文件
```
{
	"name": "Hello World",
	"version": "0.0.1",
	"author": "张三",
	"description": "第一个node.js程序",
	"keywords":["node.js","javascript"],
	"repository": {
		"type": "git",
		"url": "https://path/to/url"
	},
	"license":"MIT",
	"engines": {"node": "0.10.x"},
	"bugs":{"url":"http://path/to/bug","email":"bug@example.com"},
	"contributors":[{"name":"李四","email":"lisi@example.com"}],
	"scripts": {
		"start": "node index.js"
	},
	"dependencies": {
		"express": "latest",
		"mongoose": "~3.8.3",
		"handlebars-runtime": "~1.0.12",
		"express3-handlebars": "~0.5.0",
		"MD5": "~1.2.0"
	},
	"devDependencies": {
		"bower": "~1.2.8",
		"grunt": "~0.4.1",
		"grunt-contrib-concat": "~0.3.0",
		"grunt-contrib-jshint": "~0.7.2",
		"grunt-contrib-uglify": "~0.2.7",
		"grunt-contrib-clean": "~0.5.0",
		"browserify": "2.36.1",
		"grunt-browserify": "~1.3.0",
	}
}
```

### 二.详解每个字段的作用
大概有这么些字段
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/package.json%E8%A7%A3%E6%9E%90.png)
#### 2.1 一些基础的配置
这些就是所见即所得，看着这个单词你就可以猜出来对应的意思了。所以也就没必要展开太多的介绍。
##### 2.1.1 name 项目名称
项目包的名称，在使用的时候，可以先注册一下`npm registry`， 看这个名称是否被使用了。
##### 2.1.2 version 版本号
遵循`大版本.次要版本.小版本`的格式，比如：`1.0.0`
##### 2.1.3 author 作者
有两种写法：可以指定name,email,url也可以单独用字符串表示
```
// 方法1
{ "author": { 
    "name" : "World" , 
    "email" : "World@163.com" , 
    "url" : "http://world.com.cn/" }
}
// 方法2 
{
  "author": "World"
}
```
##### 2.1.4 keywords 关键字
添加关键字，可以在`npm search`中搜索到
##### 2.1.5 description 项目描述
##### 2.1.6 license 许可证
就是使用的许可证，比如MIT。让人知道使用的权利和限制。
##### 2.1.7 contributors 贡献者
格式和name差不多，也是有2种方式，
##### 2.1.8 main 入口文件

#### 2.2 项目相关配置
##### 2.2.1 repository 托管
##### 2.2.2 scripts 脚本
##### 2.2.3 dependencies 项目运行时所需要的依赖
##### 2.2.4 devDependencies 开发时所需要的依赖
##### 2.2.5 engines 指定模块可以运行的平台
##### 2.2.6 browser 浏览器
##### 2.2.7 config 环境变量
##### 2.2.8 bin 指定文件可执行文件的位置
##### 2.2.9 bugs 报告bug的地址或联系人
### 参考资料
- [package.json文件(阮一峰)](http://javascript.ruanyifeng.com/nodejs/packagejson.html#toc2)


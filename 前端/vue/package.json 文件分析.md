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
项目描述，可以在`npm search`中搜索到
##### 2.1.6 license 许可证
就是使用的许可证，比如MIT。让人知道使用的权利和限制。
##### 2.1.7 contributors 贡献者
格式和name差不多，也是有2种方式，
##### 2.1.8 main 入口文件
指定项目的主入口文件，一般就是项目的根目录下的index.js文件。
##### 2.1.9 private 是否是私有库
这是一种防止意外发布私有库的方式。
如果private == true ,那么 npm就不会发布它
#### 2.2 项目相关配置
##### 2.2.1 repository 托管
指明这个项目的代码会被托管在哪里，比如github。这个对想要参与项目开发的人很有用。一般是这么写的。
```
{
  "repository": {
    "type": "git",
    "url": "仓库地址"
  }
}
```
这样可以通过`npm docs`文件找到这个仓库。（应该是吧，我没试过。。哈哈哈）
##### 2.2.2 scripts 脚本
这是一个由脚本命令组成的字典。
比如命令`npm run start`,这个start的操作就是在scripts中定义的。
```
{
  "scripts": {
    "start": "node index.js"
  }
}
```

##### 2.2.3 dependencies 项目运行时所需要的依赖
这是定义了项目运行时所需要的各个依赖，指定了依赖的包名和其版本范围的映射。其中，版本范围是有一个或多个空白分割描述符的字符串。
```
{
  "dependencies": {
    "browserify": "~13.0.0",
    "karma-browserify": "~5.0.1"
  }
}
```
这里主要介绍关于版本范围的规定：
- `版本号`：比如1.0.0，这样安装的时候只会安装这个版本；
- `~版本号`：比如`~1.0.0`,表示安装1.0的最新版本（不低于1.0.0），但是不安装1.1.X，就是安装时不改变大版本号和次要版本号；
- `^版本号`：比如`^1.0.0`,表示安装1.X.X的最新版本（不低于1.0.0），但是不安装2.X.X，就是安装时不改变大版本号；
- `latest`: 最新版本

注意： `npm install`命令就是根据package.json中的配置，安装所需要的版本的依赖，但是假如你要新增一个依赖，需要单独再安装这个依赖，这时候就需要将其配置写入package.json中。
可以使用以下命令
```
// --save 表示将该模块写入dependencies属性中。
npm install express(依赖名) --save
// --save-dev 表示将该模块写入devDependencies属性中。
npm install express(依赖名) --save-dev
```
##### 2.2.4 devDependencies 开发时所需要的依赖
具体配置规则同上面，但是这个是开发时使用的依赖库。
##### 2.2.5 engines 指定模块可以运行的平台
指明了该模块运行的平台，比如node的某个版本或者浏览器。
```
{
  "engines": {
    "node": ">=0.10.3 <0.12"
  }
}
```
##### 2.2.6 browser 浏览器
##### 2.2.7 config 环境变量
用来配置脚本中的跨版本参数。
```
{
  "config": {
    "port": "8080"
  }
}
```
##### 2.2.8 bin 指定文件可执行文件的位置
这是一个命令名和本地文件名的映射，可以把许多可执行文件安装到系统路径中。
emmmm 我觉得，我自己还不太懂，就直接放我看的资料截图吧。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191101112747.png)
##### 2.2.9 bugs 报告bug的地址或联系人
对使用这个项目遇到问题的用户会有很大的帮助，可以去这里的地址提issue，反馈问题。
### 参考资料
- [package.json文件(阮一峰)](http://javascript.ruanyifeng.com/nodejs/packagejson.html#toc2)
- [(译)package.json详解(博客园-fang&&fang)](https://www.cnblogs.com/paris-test/p/9760308.html)


---
title: select2 使用介绍
tags: 插件
notebook: 前端
---
# select2 使用介绍

### 环境
- 依赖JQuery
- 需要加载 select2.min.js 和 select2.min.css

### 初始化
在select元素渲染完后，初始化select2这个插件，直接通过选择器就可以初始化。
```
$("#class_id").select2() 
```
### 多选的select盒子
select2也支持多选，只要在select标签上加`multiple="multiple"`这个属性就可以了。
效果：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190918113154.png)

### 参考资料
- [select2官方文档](https://select2.org/)


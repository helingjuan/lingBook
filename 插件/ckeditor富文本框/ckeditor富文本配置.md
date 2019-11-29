---
title: ckeditor富文本框配置
tags: 富文本框
notebook: 前端
---
# ckeditor富文本框配置
维护产品的时候，发现目前使用的富文本框是百度的，如果使用场景是很简单的那种（不用嵌入图片啊什么的），其实还是很实用的，但是遇到图片，就很麻烦了，而且让我觉得换插件最重要的原因还是：百度团队都已经不维护这个插件了，emmmm
现在不跳，留着干嘛？？

ckeditor 的优点有很多插件，你需要什么引入，然后再config.js中配置就好了。
### 复制word过来且保持word里的格式
```
// 允许acf保留所有复制过来的格式，
  //ACF的介绍：Advanced Content Filter (ACF) is a CKEditor core feature that filters incoming HTML content 
  //by transforming and deleting disallowed elements, attributes, classes and styles.
  config.allowedContent = true;
```

### 加入文本颜色更改
添加插件：
```
config.extraPlugins = 'colorbutton'
```
这个插件有一些其他插件的依赖，如果初始的时候报错了，你去把它放到plugins文件夹下就可以。
比如：panelbutton和floatpanel

### 文本对齐方式
```
  config.extraPlugins = 'justify'
```

### 图片缩放，移动
```
  config.extraPlugins = 'image2'
```

### emoji表情
哇。。这个依赖了很多东西，不是刚需，不建议用。
```
  config.extraPlugins = 'emoji'
```



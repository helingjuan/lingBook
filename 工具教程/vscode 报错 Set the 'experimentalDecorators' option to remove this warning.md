---
title: vscode 报错 Set the 'experimentalDecorators' option to remove this warning.
tags: 
notebook: 
---
# vscode 报错 Set the 'experimentalDecorators' option to remove this warning.
报错信息
```
Experimental support for decorators is a feature that is subject to change in a future release. Set the 'experimentalDecorators' option to remove this warning.
```
解释：  
就是说vscode对这个修饰器的支持是一项将会在未来版本中发布的功能，现在可以设置`experimentalDecorators`选项去除这个警告

## 处理方法
路径：文件——首选项——设置，即可打开配置，
把`javascript.implicitProjectConfig.experimentalDecorators`设为true
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191126174148.png)



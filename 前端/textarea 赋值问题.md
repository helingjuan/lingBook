---
title: textarea 赋值问题
tags: 
notebook: 前端
---
# textarea 赋值问题
突然遇到这么一个问题，textarea的赋值居然赋不上去，？？？ 它不是和input一个直接在value属性里赋值吗？
怀揣着疑问，我去找了度娘。
emmmm
来看下我的错误示范
### 错误示范
```
<textarea class="m-wrap large" name="description" placeholder="请输入运动队简介" cols="30" rows="3" value="我是第一运动队"></textarea>
```
然后就会发现？？？
是空的，根本没效果     
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190906161215.png)

### 正确示范
```
<textarea class="m-wrap large" name="description" placeholder="请输入运动队简介" cols="30" rows="3">我是第一运动队</textarea><br><br>
```
出來了
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190906161656.png)

### 原因分析
因为textarea的html标签中没有value属性。
### 参考资料
- [`<textarea>`——(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/textarea)
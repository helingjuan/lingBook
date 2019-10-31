---
title: css 伪元素和伪类的区别和联系
tags: css
notebook: 前端
---
# css 伪元素和伪类的区别和联系
总是经常混在一起，就记录一下吧。

#### Q1：伪类和伪元素的区别
伪类和伪元素的根本区别是：**他们是否创造了新的元素**
从定义来说：  
- 伪类，定义的是一个类，经常是表示状态的。存在DOM树中。常见的伪类有：`:hover`,`:active`,`:focus`,`:visited`,`:first-child`,`:last-child`,`:nth-child()`等；
- 伪元素，定义的是一个不存在于DOM数的虚拟元素，他们可以像正常的html元素一样定义css，但无法使用js获取。常见的伪元素有：`::before`,`::after`,`::first-letter`,`::first-line`等。   


**注意点：**
- **css3明确规定了，伪类用一个冒号(:)表示，伪元素用两个冒号来表示**。但是，目前因为兼容性的问题，大多数都是用一个冒号，所以就很容易混乱。（疯狂点头！！！）   
- 伪类可以同时使用多个，但是只能使用一个伪元素，且只能出现在末尾，且有些伪元素要配合content属性一起使用

##### 伪类和伪元素的效果
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191011164356.png)
```
// html
<h4>伪类和伪元素</h4>
<div class="content center">
  <div class="pseudo-demo">
    <p>我啥也没有。</p>
    <p>我用了伪类，变得更好看了</p>
    <p class="font-beauty">我不用伪类，我也一样好看，因为我加了class</p>
    <p>我用了伪元素，加了标题线</p>
    <p><span class="title">|</span>我不用伪元素，我也加了标题线，因为我加了span标签</p>
  </div>
</div>
```
```
// css
.pseudo-demo {
  line-height: 32px;
  border: 1px solid #ccc;
  padding: 20px 20px;
  position: relative;
  /* 伪类 */
  & p:nth-child(2) {
    background-color: #0B6E48;
    color:#fff;
    font-size: 18px;
    font-weight: 400;
  }
  .font-beauty {
    background-color: #0B6E48;
    color:#fff;
    font-size: 18px;
    font-weight: 400;
  }
  /* 伪元素 */
  & p:nth-child(4) {
    position: relative;
    font-weight: bold;
  }
  & p:nth-child(4)::after {
    position: absolute;
    content: '';
    width: 4px;
    height: 18px;
    top: 7px;
    left: -10px;
    background-color: #0B6E48;
  }
  .title {
    position: absolute;
    display: inline-block;
    font-size: 19px;
    font-weight: bolder;
    color: #0B6E48;
    bottom: 25px;
    left: 10px;
    line-height: 25px;
  }
}
```
ps.其实这里有两种方式替代那个标题线：
1. **添加标签，通过字体的css属性来调整样式**，但是这样有个问题，就是标题线的宽度有限，其实不是很灵活，**这里只是为了举例而这样用的**，而且从截图上也能很明显看出来是显示的效果是有限的；  
2. **利用class，通过p标签的边框，只显示左边的边框，再通过内边距的调整**，也是一种方式
3. 但是不管怎样，这些都会有些影响p标签，所以还是伪元素的方式最好了。因为伪元素是在一个相对独立的地方绘制这个元素的。可以做很多效果，就很好用啊！

##### 伪类分析
主要代码
```
<p>我用了伪类，变得更好看了</p>
<p class="font-beauty">我不用伪类，我也一样好看，因为我加了class</p>
```
```
/* 伪类 */
& p:nth-child(2) {
  background-color: #0B6E48;
  color:#fff;
  font-size: 18px;
  font-weight: 400;
}
.font-beauty {
  background-color: #0B6E48;
  color:#fff;
  font-size: 18px;
  font-weight: 400;
}
```
可以很明显的看出来，**伪类的效果可以直接用添加class的方式替代**，所以伪类就是一个类(class)
##### 伪元素的分析
主要代码
```
<p>我用了伪元素，加了标题线</p>
<p><span class="title">|</span>我不用伪元素，我也加了标题线，因为我加了span标签</p>
```
```
/* 伪元素 */
& p:nth-child(4) {
  position: relative;
  font-weight: bold;
}
& p:nth-child(4)::after {
  position: absolute;
  content: '';
  width: 4px;
  height: 18px;
  top: 7px;
  left: -10px;
  background-color: #0B6E48;
}
.title {
  position: absolute;
  display: inline-block;
  font-size: 19px;
  font-weight: bolder;
  color: #0B6E48;
  bottom: 25px;
  left: 10px;
  line-height: 25px;
}
```
可以看出，**伪元素的效果可以通过添加一个新标签（元素）或者添加class来实现**，但是这些效果都或多或少会影响其他部分的代码。所以伪元素就是伪造出一个新元素的效果（勉强这么理解吧  哈哈哈哈）
##### 伪类目录
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/1575920682-5aa8738170650_articlex.png)
##### 伪元素目录
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191011161148.png)


### 参考资料
- [伪元素和伪类的区别总结(CSDN-一晌贪欢i)](https://blog.csdn.net/qq_27674439/article/details/90608220)
- [「前端面试题系列3」伪类与伪元素的区别及实战(segmentfault-micherwa)](https://segmentfault.com/a/1190000017784553)

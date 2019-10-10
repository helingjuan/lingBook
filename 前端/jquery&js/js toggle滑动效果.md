---
title: js toggle滑动效果
tags: js
notebook: 前端
---
# js toggle滑动效果
就是用css来实现滑动效果，

```
// css
.slider {
  overflow-y: hidden;
  max-height: 500px;
  /* 最大高度 */
  background: pink;
  height: 200px;
  width: 200px;
  /*  Webkit内核浏览器：Safari and Chrome 敲重点！！！*/
  -webkit-transition-property: all;
  -webkit-transition-duration: .5s;
  -webkit-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
  /*  Mozilla内核浏览器：firefox3.5+*/
  -moz-transition-property: all;
  -moz-transition-duration: .5s;
  -moz-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
  /*  Opera*/
  -o-transition-property: all;
  -o-transition-duration: .5s;
  -o-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
  /*  IE9*/
  -ms-transition-property: all;
  -ms-transition-duration: .5s;
  -ms-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
  &.closed {
    max-height: 0;
  }
}
.no-slider {
  overflow-y: hidden;
  max-height: 500px;
  /* 最大高度 */
  background: #AAAEEB;
  height: 200px;
  width: 200px;
  &.closed {
    max-height: 0;
  }
}
.box {
  height: 200px;
  width: 200px;
  border: 1px solid #ccc;
  margin-bottom: 20px;
}
```
```
// html
<div class="content flex-row">
  <div>
    <div class="box">
      <div class="no-slider" id="noSlider">不加滑动效果</div>
    </div>
    <p class="btn" onclick="slide(1)">点击</p>
  </div>
  <div>
      <div class="box">
        <div class="slider" id="slider">加了滑动效果</div>
      </div>
      <p class="btn" onclick="slide(2)">点击</p>
  </div>
</div>
```

```
/**
 * 点击滑动
 * @param 类型 type  1：没有滑动；2 滑动
 */
var slide = function(type) {
  switch(parseInt(type)) {
    case 1: 
      document.getElementById('noSlider').classList.toggle('closed')
      break;
    case 2:
      document.getElementById('slider').classList.toggle('closed')
      break;
  }
}
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/slider.gif)

我自己的疑问点：
1. js 中classList 是什么东西
2. css 中cubic-bezier 是什么效果？盒子吗？

接下来，查资料吧。
### 问题解决
#### Q1:js 中classList 是什么东西
打个断点看看   
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191010163601.png)
那么，再来查个资料。  
> DOMTokenList 接口表示一组空格分隔的标记（tokens）。如由 Element.classList、HTMLLinkElement.relList、HTMLAnchorElement.relList 或 HTMLAreaElement.relList 返回的一组值。它和 JavaScript Array 对象一样，索引从 0 开始。——MDN

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191010163219.png)

#### Q2:css 中cubic-bezier 是什么效果？盒子吗？
css属性会收到transition（过渡）的影响，会产生不断变化的中间值，而`transition-timing-function`属性是用来描述这个中间值是怎样计算的。**也就是通过transition-timing-funtion这个属性，来创建一个变化的加速度函数，控制元素的变化速度。**   
这里又有个引申，`transition-timing-function`中的所有的参数，都来自`timing-funtion`中的定义。

效果：  
看下语法：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191009174026.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/transition-timing.gif)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/transition-timing-2.gif)

这里重点看cubic-bezier  
```cubic-bezier(x1, y1, x2, y2)```  
这是一种**定时函数：立方贝塞尔曲线**。这些曲线是连续的，一般用于**动画**的平滑变换，也被称为缓动函数(easing functions)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191010100008.png)
> Cubic Bézier curves with the P1 or P2 ordinate outside the [0, 1] range may generate bouncing effects. (P1 或者P2设置超过[0,1]的数值时，有可能产生弹跳效果。) ——MDN
效果：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191010155932.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191010160016.png)
emmmm  虽然有文档介绍了，但是还是有点懵。
### 参考资料
- [纯CSS实现滑动效果（Slide Up & Slide Down）(w3cways-牵着狗狗看MM)](https://www.w3cways.com/1166.html)
- [DOMTokenList(MDN文档-中文)](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMTokenList)
- [timing-funtion数学函数(MDN文档-中文)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/timing-function)
- [timing-funtion数学函数(MDN文档-英文-感觉更清楚)](https://developer.mozilla.org/en-US/docs/Web/CSS/timing-function)
- [transition-timing-function(MDN文档)](
https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-timing-function)


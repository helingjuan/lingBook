---
title: css 实现三角形、梯形、菱形等
tags:
notebook:
---
# css 实现三角形、梯形、菱形等
主要是利用了边框border属性，和透明属性(`transparent`),菱形稍微复杂一点点，用到了after伪元素。
## border 介绍
border 是用于设置各种边界属性的简写属性，border可以用于设置一个或多个以下属性的值：`border-width`, `border-style`, `border-color`
```
border: [border-width || border-style || border-color | inherit]
```
- border-color 如果没有设置，就默认为元素的color属性值。
  - transparent 透明

- border-style 常用的是 solid 实线。但是其实有很多不同类型的。效果如图：
  - none 不显示边框，优先级最低，如果存在其他边框重叠，会显示其他边框
  - hidden 不显示边框，优先级最高，存在边框重叠也不显示
  - dotted 由圆点组成的边框
  - dashed 由短的方形组成的边框
  - solid 实线
  - double 双实线
  - groove 有雕刻效果的边框
  - ridge 有浮雕效果的边框
  - inset 有陷入效果的边框
  - outset 有突出效果的边框

效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552466639439.png)
### 三角形原理
通过transparent 是把border颜色都先设为透明。再通过border-color 中的颜色来覆盖transparent。有设置颜色的边框部分就显示出来了。

#### 1.单独的一个div画三角形
##### 宽高100 的div
一般来说，我们用border来控制那个块的边框。主要呈现方式有，颜色与透明度，圆角(border-radius)，边框粗细，边框线的形式等。
就像这样：
```
<div class="box-100"></div>

//css
.box-100 {
  width: 100px;
  height: 100px;
  border: 20px solid transparent;
  border-color: #E08031 #199475 #0B6E48 #044D22;
}
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552470021410.png)
——可以看出来边框是一个以盒子中间的content为主的梯形。所以可以联想到当 div的宽高都为0的时候，盒子就是由边框组成，就是4个三角形。
##### 宽高为0的div
```
<div class="box-0-full"></div>

// css
.box-0-full {
  width: 0px;
  height: 0px;
  border: 50px solid transparent;
  border-color: #E08031 #199475 #0B6E48 #044D22;
}
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552470239960.png)
——这时候盒子的大小完全有边框决定。
这时候，是因为我们将border-color 设置为上下左右4个，所以有4个三角形，那么如果只是单独设置一个颜色，不就是一个三角形了吗？
##### 三角形
```
<div class="box-0-triangle"></div>

// css
.box-0-triangle {
  width: 0px;
  height: 0px;
  border: 50px solid transparent;
  border-left-color: #044D22;
}
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552470441127.png)
完成了。这就是一个由border和transparent组合成的三角形。

——以上，是要单独用个div弄个三角形，其实真正会使用到挺少的。一般来说，这个三角是在选择框中出现。其实原理都是一样的。但是有一点点区别。直接在原来的元素基础上即可，不用一个单独的盒子来描绘三角形。

那么感兴趣的请继续往下看。
#### 2. 用:after来画三角形
```
<div class="p-0-triangle">
  我想看的更多，选的更多
 </div>

// css
.p-0-triangle {
  background-color: #199475;
  font-size: 14px;
  line-height: 30px;
  border-radius: 10px;
  border: 1px solid #EFEFEF;
  position: relative;
  padding: 0 30px 0 20px;
}
.p-0-triangle:after {
  position: absolute;
  content: '';
  top: 5px;
  right: 0px;
  border: 10px solid transparent;
  border-left-color: #C7CEB2;
}
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552471514735.png)

## 汇总
直接看代码吧！其实很简单的
```
// html
<div class="center">
    <h4>css实现三角形、梯形、菱形</h4>
    <div class="content">
      <div class="flex-row">
          <div class="box-0">0px</div>
          <div class="box-10">10px</div>
          <div class="box-20">20px</div>
          <div class="box-30">30px</div>
      </div>
      <div class="flex-row">
          <div>完整版</div>
          <div class="box-0 triangle"></div>
          <div class="box-10 triangle"></div>
          <div class="box-20 triangle"></div>
          <div class="box-30 triangle"></div>
      </div>
      <div class="flex-row">
          <div>上三角</div>
          <div class="box-0 triangle-top"></div>
          <div class="box-10 triangle-top"></div>
          <div class="box-20 triangle-top"></div>
          <div class="box-30 triangle-top"></div>
      </div>
      <div class="flex-row">
          <div>右三角</div>
          <div class="box-0 triangle-right"></div>
          <div class="box-10 triangle-right"></div>
          <div class="box-20 triangle-right"></div>
          <div class="box-30 triangle-right"></div>
      </div>
      <div class="flex-row">
          <div>下三角</div>
          <div class="box-0 triangle-bottom"></div>
          <div class="box-10 triangle-bottom"></div>
          <div class="box-20 triangle-bottom"></div>
          <div class="box-30 triangle-bottom"></div>
      </div>
      <div class="flex-row">
          <div>左三角</div>
          <div class="box-0 triangle-left"></div>
          <div class="box-10 triangle-left"></div>
          <div class="box-20 triangle-left"></div>
          <div class="box-30 triangle-left"></div>
      </div>
      <div class="flex-row">
          <div>右直角</div>
          <div class="box-0 triangle-90-right"></div>
          <div class="box-10 triangle-90-right"></div>
          <div class="box-20 triangle-90-right"></div>
          <div class="box-30 triangle-90-right"></div>
      </div>
      <div class="flex-row">
          <div>左直角</div>
          <div class="box-0 triangle-90-left"></div>
          <div class="box-10 triangle-90-left"></div>
          <div class="box-20 triangle-90-left"></div>
          <div class="box-30 triangle-90-left"></div>
      </div>
      <div class="flex-row">
          <div>菱形</div>
          <div class="box-0 rhombus"></div>
          <div class="box-10 rhombus"></div>
          <div class="box-20 rhombus"></div>
          <div class="box-30 rhombus"></div>
      </div>
    </div>
  </div>
```
```
// css
.content {
  height: auto !important;
  div {
    margin-top: 10px;
    margin-right: 30px;
  }
  .triangle {
    border-top: 25px solid blue;
    border-left: 25px solid yellow;
    border-right: 25px solid gray;
    border-bottom: 25px solid black;
  }
  .triangle-left {
    border-top: 25px solid transparent;
    border-left: 25px solid yellow;
    border-right: 25px solid transparent;
    border-bottom: 25px solid transparent;
  }
  .triangle-right {
    border-top: 25px solid transparent;
    border-left: 25px solid transparent;
    border-right: 25px solid gray;
    border-bottom: 25px solid transparent;
  }
  .triangle-top {
    border-top: 25px solid blue;
    border-left: 25px solid transparent;
    border-right: 25px solid transparent;
    border-bottom: 25px solid transparent;
  }
  .triangle-bottom {
    border-top: 25px solid transparent;
    border-left: 25px solid transparent;
    border-right: 25px solid transparent;
    border-bottom: 25px solid black;
  }
  .triangle-90-left {
    border-left: 25px solid yellow;
    border-bottom: 25px solid yellow;
    border-right: 25px solid transparent;
    border-top: 25px solid transparent;
  }
  .triangle-90-right {
    border-right: 25px solid gray;
    border-bottom: 25px solid gray;
    border-left: 25px solid transparent;
    border-top: 25px solid transparent;
  }
  .rhombus {
    border-right: 25px solid black;
    border-top: 25px solid transparent;
    border-left: 25px solid transparent;
    border-bottom: 25px solid transparent;
    position: relative;

  }
  .rhombus::after {
    content: '';
    position: absolute;
    top: -24px;
    left: 25px;
    border-left: 25px solid black;
    border-top: 25px solid transparent;
    border-right: 25px solid transparent;
    border-bottom: 25px solid transparent;
  }
  .box-0.rhombus::after {
    width: 0px;
    height: 0px;
  }
  .box-10.rhombus::after {
    width: 10px;
    height: 10px;
    left: 35px;
  }
  .box-20.rhombus::after {
    width: 20px;
    height: 20px;
    left: 45px;
  }
  .box-30.rhombus::after {
    width: 30px;
    height: 30px;
    left: 55px;
  }
  .box-0 {
    width: 0px;
    height: 0px;
  }
  .box-10 {
    width: 10px;
    height: 10px;
  }
  .box-20 {
    width: 20px;
    height: 20px;
  }
  .box-30 {
    width: 30px;
    height: 30px;
  }
}
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191130095351.png)

## 参考资料
- [border-style(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-style)
- [css中元素border属性的构成以及配合属性值transparent可得到一些特殊形状1.0 (博客园 - JaggerGuo)](https://www.cnblogs.com/JaggerG/p/6819463.html)


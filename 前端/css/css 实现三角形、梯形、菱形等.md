---
title: css 实现三角形、梯形、菱形等
tags: 
notebook: 
---
# css 实现三角形、梯形、菱形等
主要是利用了边框border属性，和透明属性(`transparent`),菱形稍微复杂一点点，用到了after伪元素。  
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
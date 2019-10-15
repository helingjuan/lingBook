---
title: css动画 图片翻转技巧解析
tags: css
notebook: 前端
---
# css动画 图片翻转技巧解析
就是当鼠标移入图片上方的时候，可以看到图片背面的信息。鼠标移出时，又恢复原样。
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/flipAnimation.gif)

代码：  
```
// css
.filp-container-y {
  perspective: 1000px;
  &:hover .flipper,&.hover .flipper {
    transform: rotateY(180deg);
  }
  /* 翻转速度 */
  .flipper {
    transition: 0.6s;
    transform-style: preserve-3d;
    position: relative;
    .front, .back {
      backface-visibility: hidden;
      position: absolute;
      top: 0;
      left: 0;
    }
    /* 窗口正面 */
    .front {
      z-index: 2;
      transform: rotateY(0deg);
    }
    /* 窗口背面 */
    .back {
      transform: rotateY(180deg)
    }
  }
}
.filp-container-y,.filp-container-y .front,.filp-container-y .back {
  width: 320px;
  height: 480px;
  border: 1px solid #ccc;
}
/* 竖着转 */
.filp-container-x,.filp-container-x .front,.filp-container-x .back {
  width: 320px;
  height: 400px;
  border: 1px solid #ccc;
}
.filp-container-x {
  perspective: 1000px;
  &:hover .flipper,&.hover .flipper {
    transform: rotateX(-180deg);
  }
  /* 翻转速度 */
  .flipper {
    transition: 0.6s;
    transform-style: preserve-3d;
    position: relative;
    transform-origin: 100% 200px; /*是容器高度的一半*/
    .front, .back {
      backface-visibility: hidden;
      position: absolute;
      top: 0;
      left: 0;
    }
    /* 窗口正面 */
    .front {
      z-index: 2;
      transform: rotateX(0deg);
    }
    /* 窗口背面 */
    .back {
      transform: rotateX(180deg)
    }
  }
}
```
```
// html
<div class="center">
  <h4>css动画，图片翻转</h4>
  <div class="content flex-row">
    <!-- ontouchstart :允许在触摸屏上交互 -->
    <div class="filp-container-y" ontouchstart="flip(this)">
      <div class="flipper">
        <div class="front bg-199475 center">
          <!-- 图片正面 -->
          <span>我是正面正面-横着转</span>
        </div>
        <div class="back bg-minions-2 center">
          <!-- 图片背面 -->
          <span>背面-看什么看！</span>
        </div>
      </div>
    </div>
    <div class="filp-container-x margin-left-50" ontouchstart="flip(this)">
      <div class="flipper">
        <div class="front bg-199475 center">
          <!-- 图片正面 -->
          <span>我是正面正面-竖着转</span>
        </div>
        <div class="back bg-nonra-1 center">
          <!-- 图片背面 -->
          <span>背面</span>
        </div>
      </div>
    </div>
    <div></div>
  </div>
</div>
```
```
// js
var flip = function(tag) {
  tag.classList.toggle('hover');
}
```
#### 代码分析
重点部分：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191015175341.png)

### 参考资料
- [CSS图片翻转动画技术详解(WEB骇客)](http://www.webhek.com/post/css-flip.html)
- [Create a CSS Flipping Animation(DWB-这是上面的英文原版)](https://davidwalsh.name/css-flip)
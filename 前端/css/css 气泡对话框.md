---
title: css 气泡对话框
tags: 组件
notebook: 前端
---
# css 气泡对话框
做这个的前提是，你知道怎么用css实现三角形，如果还不太清楚的话看这个[](),或者直接看也可以。
## 原理分析
其实这个就是由一个div，内嵌一个三角形，再通过绝对定位来摆造型。  
是不是很简单！那就看代码吧
```
// html
<div class="center">
    <h4>css气泡对话框</h4>
    <div class="content">
      <div class="pop-dialog">
        <span class="triangle-bottom"></span>
        <p>灰色的下三角</p>
      </div>
      <div class="pop-dialog">
        <span class="triangle-bottom-shadow"></span>
        <p>和气泡背景同色的的下三角</p>
      </div>
      <div class="pop-dialog">
        <span class="triangle-right"></span>
        <p>长一点的左三角</p>
      </div>
      <div class="pop-dialog">
        <span class="triangle-left"></span>
        <p>长一点的右三角</p>
      </div>
    </div>
  </div>
```
```
// css
.content {
  height: auto !important;
  .pop-dialog {
    width: 200px;
    height: 100px;
    border-radius: 15px;
    background-color: #FEFCF8;
    margin: 20px;
    position: relative;
    padding: 20px;
    color: #606366;
  }
  .triangle-bottom, .triangle-bottom-shadow {
    position: absolute;
    top: -20px;
    left: 10px;
    width: 0;
    height: 0;
    border-top: 10px solid transparent;
    border-right: 10px solid transparent;
    border-bottom: 10px solid gray;
    border-left: 10px solid transparent;
  }
  .triangle-bottom-shadow {
    border-bottom: 10px solid #FEFCF8;
  }
  .triangle-right {
    position: absolute;
    top: 20px;
    right: -30px;
    width: 0;
    height: 0;
    border-top: 10px solid transparent;
    border-right: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 20px solid #FEFCF8;
  }
  .triangle-left {
    position: absolute;
    top: 20px;
    left: -30px;
    width: 0;
    height: 0;
    border-top: 10px solid transparent;
    border-left: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-right: 20px solid #FEFCF8;
  }
}
```
效果：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191130105011.png)

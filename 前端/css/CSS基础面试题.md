# CSS面试相关

<!-- TOC -->

- [CSS面试相关](#css面试相关)
  - [一. CSS基础](#一-css基础)
    - [1.介绍一下标准的css的盒子模型？与低版本IE的盒子模型有什么不同？](#1介绍一下标准的css的盒子模型与低版本ie的盒子模型有什么不同)
    - [2. box-sizing属性（不怎么用）](#2-box-sizing属性不怎么用)
    - [3. css选择器有哪些？哪些属性可以继承？](#3-css选择器有哪些哪些属性可以继承)
      - [css选择器](#css选择器)
      - [可以继承的属性](#可以继承的属性)
      - [不可继承的属性](#不可继承的属性)
    - [4. CSS优先级算法如何计算？:question:](#4-css优先级算法如何计算)
    - [5. 如何居中div?如何居中一个浮动元素？如何让绝对定位的div居中？](#5-如何居中div如何居中一个浮动元素如何让绝对定位的div居中)
      - [绝对定位的div居中](#绝对定位的div居中)
    - [6. display有哪些值？说明他们的作用？](#6-display有哪些值说明他们的作用)
    - [7. position的值？](#7-position的值)
    - [8. 用纯css创建一个三角形的原理是什么？](#8-用纯css创建一个三角形的原理是什么)
    - [9. 一个满屏品字布局如何设计？](#9-一个满屏品字布局如何设计)
    - [10. 常见的兼容性问题？:exclamation::exclamation::exclamation:](#10-常见的兼容性问题️️️)
    - [11. 为什么要初始化CSS样式？](#11-为什么要初始化css样式)
    - [12. absolute的containing block计算方式和正常流有什么不同？:question:（这个题我就没看懂。。。）](#12-absolute的containing-block计算方式和正常流有什么不同这个题我就没看懂)
    - [13. CSS里的visibility属性的collapse属性值的作用？在不同浏览器下有什么区别？:question:](#13-css里的visibility属性的collapse属性值的作用在不同浏览器下有什么区别)
    - [14. display:none 和visibility：hidden的区别？:star::star::star::star::star:(超高频)](#14-displaynone-和visibilityhidden的区别️️️️️超高频)
    - [15. position和display、overflow、float这些特性相互叠加后会怎样？](#15-position和displayoverflowfloat这些特性相互叠加后会怎样)
    - [16. 对BFC规范（block formatting context：块级格式化上下文）的理解？:question:](#16-对bfc规范block-formatting-context块级格式化上下文的理解)
      - [什么是BFC？](#什么是bfc)
        - [box：css布局的基本单位](#boxcss布局的基本单位)
        - [formatting context:一个决定如何渲染文档的容器](#formatting-context一个决定如何渲染文档的容器)
      - [如何触发BFC？](#如何触发bfc)
      - [BFC的作用](#bfc的作用)
    - [17. 上下margin重合的问题](#17-上下margin重合的问题)
    - [18. 为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式？:question:](#18-为什么会出现浮动和什么时候需要清除浮动清除浮动的方式)
      - [为什么会出现浮动？](#为什么会出现浮动)
      - [什么时候需要清除浮动？](#什么时候需要清除浮动)
      - [清除浮动的方式](#清除浮动的方式)
    - [19. 设置元素浮动后，该元素的display值是多少？](#19-设置元素浮动后该元素的display值是多少)
    - [20. 移动端的布局用过媒体查询吗？](#20-移动端的布局用过媒体查询吗)
    - [21. 有哪些CSS预处理器？](#21-有哪些css预处理器)
    - [22. CSS优化、提高性能的方法有哪些？:question:](#22-css优化提高性能的方法有哪些)
    - [23. 浏览器是怎样解析CSS选择器的？:question:](#23-浏览器是怎样解析css选择器的)
    - [24. 在网页中的字体大小应该使用奇数还是偶数？为什么呢？](#24-在网页中的字体大小应该使用奇数还是偶数为什么呢)
    - [25，margin和padding分别适合什么场景使用？](#25margin和padding分别适合什么场景使用)
    - [26.元素竖向的百分比设定是相对于容器的高度吗？](#26元素竖向的百分比设定是相对于容器的高度吗)
    - [27. 全屏滚动的原理是什么？用到了css的那些属性？](#27-全屏滚动的原理是什么用到了css的那些属性)
    - [28. 什么是响应式设计？什么是自适应？响应式设计的基本原理是什么？如何兼容低版本的IE？](#28-什么是响应式设计什么是自适应响应式设计的基本原理是什么如何兼容低版本的ie)
      - [什么是响应式设计？](#什么是响应式设计)
      - [什么是自适应？](#什么是自适应)
      - [响应式和自适应的区别？](#响应式和自适应的区别)
      - [响应式原理](#响应式原理)
      - [如何兼容低版本的IE？](#如何兼容低版本的ie)
    - [29. 视差滚动效果？:question:](#29-视差滚动效果)
      - [什么是视差滚动？](#什么是视差滚动)
      - [如何实现？](#如何实现)
    - [30. ::before和：after中双冒号和单冒号有什么区别？解释一下这两个伪元素的作用](#30-before和after中双冒号和单冒号有什么区别解释一下这两个伪元素的作用)
      - [单冒号和双冒号的区别？](#单冒号和双冒号的区别)
      - [::before 和::after 的作用](#before-和after-的作用)
    - [31. 对line-height如何理解？](#31-对line-height如何理解)
    - [32.怎么让Chrome支持小于12px的字体？:question:](#32怎么让chrome支持小于12px的字体)
    - [33. 让页面里的字体变清晰，变细用css怎么做？:question:](#33-让页面里的字体变清晰变细用css怎么做)
    - [34. position:fixed 在安卓下无效怎么处理？:question:](#34-positionfixed-在安卓下无效怎么处理)
    - [35. 如果需要手写动画，你认为最小时间间隔是多少？为什么？](#35-如果需要手写动画你认为最小时间间隔是多少为什么)
    - [36. display：inline-block什么时候会显示间隙？](#36-displayinline-block什么时候会显示间隙)
    - [37. 有一个高度自适应的div，里面有两个div,一个高度100px，希望另一个填满剩下的高度](#37-有一个高度自适应的div里面有两个div一个高度100px希望另一个填满剩下的高度)
    - [38. png,jpg,gif 这些图片格式解释一下,分别什么时候用？有没有了解过webp？](#38-pngjpggif-这些图片格式解释一下分别什么时候用有没有了解过webp)
    - [39. style标签写在body后和body前有什么区别？](#39-style标签写在body后和body前有什么区别)
      - [如果放在body后会有什么问题？](#如果放在body后会有什么问题)
    - [40. css属性overflow属性定义一处元素内容区的内容会如何处理？](#40-css属性overflow属性定义一处元素内容区的内容会如何处理)
    - [41.阐述一下css Sprites（雪碧图）](#41阐述一下css-sprites雪碧图)
  - [二. CSS3相关](#二-css3相关)
    - [1. CSS3新增伪类有哪些？:question:](#1-css3新增伪类有哪些)
    - [2. CSS3有哪些新特性？:question:](#2-css3有哪些新特性)
    - [3. 请解释一下CSS3的 flexbox(弹性盒布局模型),以及适用场景？](#3-请解释一下css3的-flexbox弹性盒布局模型以及适用场景)
- [参考资料](#参考资料)

<!-- /TOC -->
## 一. CSS基础

### 1.介绍一下标准的css的盒子模型？与低版本IE的盒子模型有什么不同？

标准盒子模型：宽度 = 内容的宽度(content) + border + padding + margin
低版本IE盒子模型：宽度 = 内容的宽度（content+border+padding） + margin
最主要的区别就是**内容宽度的计算**

### 2. box-sizing属性（不怎么用）

用来控制元素的盒子模型的解析模式，默认为`content-box`
属性值：

- `content-box`:W3C的标准盒子模型，元素的宽高就是content部分的宽高
- `border-box`:IE传统盒子模型，元素的宽高指的是border+padding+border部分的宽高

### 3. css选择器有哪些？哪些属性可以继承？

#### css选择器

- id选择器（#myBox）
- 类选择器（class选择器，.myBox）
- 标签选择器（div等）
- 相邻选择器（div + p）:question:
- 子选择器(ul > li):question:
- 后代选择器(ul li)
- 通配符选择器（*）
- 属性选择器(a[rel="external"]):question:
- 伪类选择器(:hover, :nth-child)

**选择器的优先级**(就近原则)
`!important > [id > class > tag ]`

#### 可以继承的属性

- font-size
- font-family
- color

#### 不可继承的属性

- boder
- padding
- margin
- width
- height

### 4. CSS优先级算法如何计算？:question:
计算权重：
- 元素选择符：1
- class选择符： 10
- id选择符：100
- 元素标签： 1000

计算规则：
- `!important`声明的样式优先级最高，如果冲突再计算
- 如果优先级相同，则选择最后出现的样式（渲染时离的最近的样式）
- 继承得到的样式的优先级最低

### 5. 如何居中div?如何居中一个浮动元素？如何让绝对定位的div居中？
居中有水平、垂直，水平垂直居中
1. **水平居中**：
  - 如果div内只有文字的话，且文字较少,可以用`text-align:center;`
  - flex布局
    ```
    display: flex;
    justify-content: center;
    ```
  - 通用
    ```
    width: 50px;
    height: 50px;
    margin: 0 auto; // 最关键的
    ```
2. **垂直居中**
- 如果div内只有文字的话，且文字较少，可以用`line-height`\
- flex布局
  ```
  display: flex;
  align-item: center;
  ```
- 通用`margin: auto 0;`

1. **水平垂直居中**
   - flex布局(强烈推荐！)
      ```
        // 父元素
        .box {
          display: flex;
          justify-content: center;
          align-item: center;
        }
      ```
   - 绝对定位
      ```
      // 子元素(居中一个浮动元素)
      .box-child {
        position: absolute;
        float: left;
        left: 50%;
        right: 50%;
        height: 100px;
        width: 200px;
        margin: -50px 0 0 -100px;
      }
      ```

#### 绝对定位的div居中
```
.box-child {
  position: absolute;
  width: 200px;
  height: 100px;
  margin: 0 auto;
  left: 0;
  right: 0;
}
```

### 6. display有哪些值？说明他们的作用？

属性值：

- block 块元素
- inline-block 行内的块元素
- inline 内联
- none 隐藏
- table 表格
- list-item 项目列表

### 7. position的值？
属性值：
- relative 相对定位，不脱离文档流，参考自身静态位置通过top，bottom，left，right 进行定位
- absolute 绝对定位，参考距离最近一个不为static的父级元素，通过上下左右进行定位
- fixed 固定定位，参考可视窗口进行定位
- static 默认，按照正常的文档流进行排列

### 8. 用纯css创建一个三角形的原理是什么？
原理，border边框，伪元素和透明属性,div的宽高都为0的时候，盒子就是由边框组成，就是4个三角形,将边框先都设置成透明，然后把要实现的那个方向的三角形赋上颜色，即可
```
<div class="p-0-triangle">
  我想看的更多，选的更多
 </div>
// 方法一
// 当盒子宽高不为0时，画三角形
// 通过伪元素，透明元素和border来实现
.p-0-triangle {
  background-color: #199475;
  font-size: 14px;
  line-height: 30px;
  border-radius: 10px;
  border: 1px solid #EFEFEF;
  position: relative;
  padding: 0 30px 0 20px;
}
.p-0-triangle::after {
  position: absolute;
  content: '';
  top: 5px;
  right: 0px;
  border: 10px solid transparent;
  border-left-color: #C7CEB2;
}

// 方法二
// 当盒子宽高为0时，画三角形
// 通过border和透明元素来实现
// 当块元素的宽高都为0时，该块元素的大小由边框和padding决定，默认 padding是0，所以就是border，先将border都设置成透明，然后再将要显示的那个方向的三角形赋上颜色即可。
.p-0-triangle {
  width: 0px;
  height: 0px;
  border: 50px solid transparent;
  border-left-color: #044D22;
}
```

### 9. 一个满屏品字布局如何设计？
第一种真正的品字
  1. 三块宽高是确定的
  2. 上面那块用`margin: 0 auto;`居中
  3. 下面两块用float，或者inline-block或flex 不换行
  4. float和inline-block 用margin 使他们居中
  5. flex的话，就用flex属性使他们居中

第二种全屏的品
  1. 上面div的宽设置成100%
  2. 下面的div分别宽50%，可使用方法有float，inline-block,flex

### 10. 常见的兼容性问题？:exclamation::exclamation::exclamation:
1. 不同浏览器的标签默认的margin和padding不一样
   解决方法：通配符选择器 
   ```
   * {
    margin: 0;
    padding: 0;
   }
   ```
2. 获取自定义属性的方法
     - IE
       - 使用获取常规属性的方法来获取
       - 使用`getAttribute()`获取
     - FireFox
       - 只能使用`getAttribute()`获取

    **解决方法**： 统一都用`getAttribute()`来获取

3. 字体大小小于12px
   Chrome会默认将小于12px的文本强制按照12px显示
   解决方法：加入css属性`-webkit-text-size-adjust: none;`

4. 超链接访问过后hover样式不出现了，被点击访问过的超链接样式不再具有hover和active了。
解决方法： 改变CSS属性的排列顺序`:link , :visited ,:hover, :active`

### 11. 为什么要初始化CSS样式？
因为不同浏览器的标签默认的margin和padding不一样，如果不初始化，就会出现浏览器之间的页面存在差异的情况 。

### 12. absolute的containing block计算方式和正常流有什么不同？:question:（这个题我就没看懂。。。）
1，先找到其祖先元素中最近的position不为static的元素，
   - 找到祖先元素，然后判断：
     - 该元素是inline元素吗？
       - 是，则containing block为能够包含这个元素生成的第一个和最后一个inline元素的padding box（除margin，border外的区域）的最小矩形；
       - 否，就有这个祖先元素的padding box组成
   - 没找到祖先元素，则为默认containing block

### 13. CSS里的visibility属性的collapse属性值的作用？在不同浏览器下有什么区别？:question:
当一个元素`visibility: collapse;`时，对于一般元素来说，它的表现和hidden是一样的。就是隐藏了。

不同浏览器下的作用：
- Chrome, 和`visibility: hidden;`没有区别
- FireFox、Opera和IE，使用collapse和使用`display: none;` 没有区别

### 14. display:none 和visibility：hidden的区别？:star::star::star::star::star:(超高频)

- `display: none;`不显示元素，在文档流中不再分配空间（回流+重绘）
- `visibility: hidden;`隐藏元素，在文档流中仍保留原来的空间（重绘）

### 15. position和display、overflow、float这些特性相互叠加后会怎样？

- display 规定元素应该生成的框的类型
- position 规定元素的定位类型
- overflow 定义元素超出是否隐藏
- float 定义元素在哪个方向浮动

叠加的时候，就是**类似于优先级机制**，
`position: absolute/fixed` 优先级最高，有他们在时，float不起作用，display值需要调整。
float或者absolute 定位的元素，只能是块元素或者表格

### 16. 对BFC规范（block formatting context：块级格式化上下文）的理解？:question:
BFC规范，**规定了内部的块元素如何布局**，决定了其子元素如何定位，以及和其他元素的关系和相互作用。
#### 什么是BFC？
先了解一下box、formatting context的概念
##### box：css布局的基本单位
元素的类型和display属性，决定了这个盒子的类型。不同类型的盒子，会参与不同的Formatting Context，因此盒子内的元素会以不同的方式渲染
盒子的类型：
  - `block-level`
    - display值为block,list-item,table的元素，并参与**block formatting context（简称BFC）**
  - `inline-level`
    - display值为inline，inline-block，inline-table的元素，并参与**inline formatting context（简称IFC）**
  - `run-in` css3中才有

##### formatting context:一个决定如何渲染文档的容器
这是页面中的一块**渲染区域**，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用

布局规则：
  1. 内部的盒子会在垂直方向上一个接一个放置;
  2. 盒子垂直方向的距离由margin决定，**属于同一个BFC的两个相邻的margin会发生重叠**;
  3. 每个元素的margin box的左边，与包含块border box的左边相接触;
  4. BFC的区域不会与float box重叠;
  5. BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素;
  6. 计算BFC的高度时，浮动元素也会参与计算;

#### 如何触发BFC？
满足以下条件之一的就可触发BFC

  - 根元素，即html;
  - float的值不为none;
  - overflow的值不为visible
  - display的值为block,list-item,table，inline-block，table-cell，table-caption，flex或inline-flex；
  - position的值为absolute或fixed

#### BFC的作用
1. 利用BFC避免margin重叠
2. 自适应两栏布局

**总结**：
因为BFC内部的元素和外部的元素绝对不会互相影响。因此，当BFC外部存在浮动时，它不应该影响BFC内部的布局，BFC会通过变窄，而不与浮动有重叠；
同样，当BFC内部有浮动时，为了不影响外部元素的布局，BFC计算高度时会包括浮动的高度。避免margin重叠也是同样道理。

### 17. 上下margin重合的问题
解决方法： 在重合元素外包裹一层容器，并触发该容器生成一个**BFC**

```
<div class="aside"></div>
<div class="text">
    <div class="main"></div>
</div>
<!--下面是css代码-->
 .aside {
      margin-bottom: 100px;  
      width: 100px;
      height: 150px;
      background: #f66;
  }
  .main {
      margin-top: 100px;
      height: 200px;
      background: #fcc;
  }
    .text{
      /*盒子main的外面包一个div，通过改变此div的属性使两个盒子分属于两个不同的BFC，以此来阻止margin重叠*/
      overflow: hidden;  //此时已经触发了BFC属性。
  }
```

### 18. 为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式？:question:
#### 为什么会出现浮动？
浮动元素碰到包含它的边框或者浮动元素的边框停留。由于浮动元素不在文档流中，所以文档流的边框表现的就像浮动框不存在一样，浮动元素会漂浮在文档流的边框上。

#### 什么时候需要清除浮动？
因为浮动有时候会带来一些问题，比如：
- 父元素的高度无法被撑开，影响与父元素同级的元素
- 与浮动匀速同级的非浮动元素，会跟随其后
- 若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构

#### 清除浮动的方式

- 父级div定义height
- 最后一个浮动元素后加空div标签，并添加样式`clear: both;`
- 包含浮动元素的父标签添加样式`overflow: hidden或者auto`
- 父级div定义zoom
  
### 19. 设置元素浮动后，该元素的display值是多少？
自动变成`display: block;`

### 20. 移动端的布局用过媒体查询吗？
用过，通过媒体查询可以为不同大小和尺寸的媒体定义不同的css，适应相应的设备的显示。
方法：
1. head 里
   `<link rel="stylesheet" type="text/css" href="xxx.css" media="only screen and (max-device-width:480px)">`
2. css
  `@media only screen and (max-device-width:480px) {/css样式/}`

### 21. 有哪些CSS预处理器？
- **Sass** 
  2007年诞生，最早也是**最成熟**的CSS预处理器，目前已经进化到了全面兼容CSS的Scss
  有两种语法：
    - `.sass`
    - `.scss`(这个是我常用的！兼容性较好)
  Sass兼容css，可以按css方式写，也可以按sass方式或scss方式写，**最终他们都会被编译成标准css**
- Less
  2009年诞生，比起Sass来说，可编程功能不够，但是使用简单且兼容CSS。反过来影响Sass演变到Scss的过程
- Stylus
  2010年诞生，主要用来给node项目进行css预处理支持。

### 22. CSS优化、提高性能的方法有哪些？:question:
1. 避免过度约束
2. 避免后代选择符
3. 避免链式选择符
4. 使用紧凑的语法
5. 避免不必要的命名空间
6. 避免不必要的重复
7. 最好使用表示语义的名字，一个好的类名，应该是描述他是什么而不是像什么
8. 避免`!important`, 可以选择其他选择器
9. 尽可能的精简规则，可以合并不同类里的重复规则

### 23. 浏览器是怎样解析CSS选择器的？:question:
解析过程：
   1. css解析
    CSS选择器的解析是**从右向左**解析的。若从左到右的匹配，发现不符合规则，需要进行回溯，会损失很多性能；而从右到左，先找到所有最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。
    这两种匹配规则的性能差别很大，因为从右向左的匹配在第一部就筛掉了大量的不符合条件的最后节点，而从左向右的匹配规则的性能都浪费在了失败的查找上面。
   2. 建立渲染树
    在css解析完毕后，需要将解析的结果与DOM 树的内容一起进行分析建立一颗渲染树，最终用来进行绘图。在建立渲染树的时候，浏览器就要为每个DOM树中的元素根据CSS的解析结果来确定生成怎样的渲染树

### 24. 在网页中的字体大小应该使用奇数还是偶数？为什么呢？
偶数比较好，因为偶数字号相对更容易和web设计的其他部分构成比例关系。
windows自带的点阵宋体从Vista开始只提供12、14、16px这三个大小的点阵，而13、15、17px时用的是小一号的点（即每个字占的空间大了1px，但是点阵没变），于是会略显稀疏。
### 25，margin和padding分别适合什么场景使用？
margin场景：
  1. 需要在border外侧添加空白；
  2. 空白处不需要背景色；
  3. 上下相连的两个盒子之间的空白，需要相互抵消时

padding场景：
  1. 需要在border内侧添加空白；
  2. 空白处需要背景色；
  3. 上下相连的两个盒子的空白，希望为两者之和

兼容性问题：在IE5 IE6中，为float的盒子指定margin时，左侧的margin可能会变成两倍的宽度。通过改变padding或者指定盒子的display：inline解决。
### 26.元素竖向的百分比设定是相对于容器的高度吗？
当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的。
但是对于一些**表示竖向距离的属性**，比如`padding-top`,`padding-bottom`,`margin-top`,`margin-bottom`等，当按百分比设定它们时，依据的也是**父容器的宽度**，而不是高度。
但是height还是相对于父容器的高度计算的。
### 27. 全屏滚动的原理是什么？用到了css的那些属性？
**原理**：类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那个高度时500%，只是展示100%，剩下的可以通过`transform`进行y轴定位，也可以通过margin-top实现
用了哪些属性？
```
overflow: hidden;
transition: all 1000ms ease;
```
### 28. 什么是响应式设计？什么是自适应？响应式设计的基本原理是什么？如何兼容低版本的IE？
#### 什么是响应式设计？
就是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。
实现不同屏幕分辨率的终端上浏览网页，会有不同的展示方式。
#### 什么是自适应？

#### 响应式和自适应的区别？
响应式布局：就是流动网格布局；自适应布局就是使用固定分割点来进行布局。
响应式相当于液体，它可以自动适应不同尺寸的屏幕。使用css媒体查询的方法，根据目标设备自动变化风格，如显示类型、宽度、高度等，这能很好的解决不同屏幕尺寸的显示问题。
自适应设计是基于断点使用静态布局，一旦页面被加载就无法再进行自动适应，自适应会自动检测屏幕的大小来加载适当的工作布局。也就是，采用自适应设计网站时，要先设计6种常见的屏幕布局。
> 6种常见的屏幕布局
- 320 
- 480
- 760
- 960
- 1200
- 1600

**总结**：
自适应一般用于改造网站，在现有基础上兼容某尺寸的屏幕。
如果只是考虑屏幕兼容问题，首选响应式设计，但是如果预算充足，其实自适应的效果是更好的。

#### 响应式原理
通过**媒体查询**检测不同的设备屏幕尺寸做处理
#### 如何兼容低版本的IE？
页面头部加上meta声明的viewport
`<meta name=’viewport’ content=”width=device-width, initial-scale=1. maximum-scale=1,user-scalable=no”>`
### 29. 视差滚动效果？:question:
#### 什么是视差滚动？
视差滚动，就是通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的3D效果。
#### 如何实现？
方法：
1. CSS3实现
   优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器
2. jQuery实现
   通过控制不同层滚动速度，计算每一层的时间，控制滚动效果；
   优点： 能兼容到哥哥版本的，效果可控性好；缺点，开发起来对制作者的要求高
3. 插件实现`parallax-scrolling`

### 30. ::before和：after中双冒号和单冒号有什么区别？解释一下这两个伪元素的作用
#### 单冒号和双冒号的区别？
一般来说单冒号是伪类，双冒号是伪元素。伪类就是，加上一个类的效果；伪元素就是创建一个虚拟的元素，js访问不到的元素。

#### ::before 和::after 的作用
- `::before` 就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素，不存在于DOM，只存在页面中
- `::after`,定义在元素主体内容之后的一个伪元素。一般和绝对定位一起使用。
### 31. 对line-height如何理解？
就是行高啊，就是两行文字间基线的距离。
css中起高度作用的是height和line-height，没有定义height属性，最终其表现作用一定是line-height

作用：
- 单行文本垂直居中

### 32.怎么让Chrome支持小于12px的字体？:question:
```
p {
  font-size:10px;
  -webkit-transform:scale(0.8); // 缩放
} //0.8是缩放比例
```
### 33. 让页面里的字体变清晰，变细用css怎么做？:question:
```
webkit-font-smoothing在window系统下没有起作用，但是在IOS设备上起作用-webkit-font-smoothing：antialiased是最佳的，灰度平滑。
```
### 34. position:fixed 在安卓下无效怎么处理？:question:
```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>
```
### 35. 如果需要手写动画，你认为最小时间间隔是多少？为什么？
```
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms。
```
### 36. display：inline-block什么时候会显示间隙？
1. 有空格时候
   解决方法： 移除空格
2. margin正值的时候
  解决方法：margin使用负值
3. 使用font-size的时候
   解决方法：font-size、letter-spacing、word-spacing
### 37. 有一个高度自适应的div，里面有两个div,一个高度100px，希望另一个填满剩下的高度
使用**绝对定位**。
外层div设置`position: relative`
内层div，高度自适应那个
```
.div {
  position: absolute;
  top: 100px;
  right: 0;
  left: 0;
  bottom: 0;
}
```
### 38. png,jpg,gif 这些图片格式解释一下,分别什么时候用？有没有了解过webp？
图片分为位图和矢量图，位图主要由点阵组成，矢量图主要是由点线面等基于计算的方式来显示的。
位图有这么几种类型：
- png 主要用于透明色背景，和颜色比较简单的图片
- jpg 主要用于色彩丰富的图片，比如风景图等
- gif 主要用于动画
- webp（这是比较新的一种格式，较轻量，缺点是兼容性不太好，目前只有火狐支持，IE和Safari均不支持）

### 39. style标签写在body后和body前有什么区别？
html解析的顺序是，自上而下，所以肯定要先加载样式啊！
#### 如果放在body后会有什么问题？
当浏览器解析到写在尾部的样式表，会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在windows的IE下可能会出现FOUC现象，就是**页面闪烁问题**。
### 40. css属性overflow属性定义一处元素内容区的内容会如何处理？
属性值：
- `scroll` 出现滚动条
- `auto` 超出的话，出现滚动条
- `visible` 溢出的内容出现在父元素之外
- `hidden` 溢出也不出现滚动条，且隐藏溢出部分内容
### 41.阐述一下css Sprites（雪碧图）
这是网站资源加载优化的一种方式，
就是将多个图片放在一个大图里，然后通过css的background-image,background-repeat, background-position，的组合进行定位某一个图片，
这样多个图片就可以只用一次资源请求即可。大大提高了页面的性能。

## 二. CSS3相关

### 1. CSS3新增伪类有哪些？:question:

- `:first-of-type` 选择属于其父元素的首个元素
- `:last-of-type` 选择属于其父元素的最后一个元素
- `:only-of-type` 选择属于其父元素的唯一的元素
- `:only-child` 选择属于其父元素的唯一子元素
- `:nth-child(n)` 选择其属于父元素的所有子元素。n是从1开始计算的
- `:enabled`,`:disabled` 表单控件的禁用状态
- `:checked` 单选框活复选框被选中的样式


### 2. CSS3有哪些新特性？:question:
1. rgba 和透明度
2. 背景属性
   - background-image,这个可以设置渐变背景
   - background-origin(content-box/padding-box/border-box)
   - background-size
   - background-repeat
3. word-wrap 允许长的内容可以自动换行
   属性值： 
   - break-word 在长单词或URL地址内部进行换行
   - normal 默认值，只在允许断字典换行（浏览器保持默认处理）
4. font-face 定义自己的字体
5. border-radius 圆角
6. border-image 边框图片
7. text-shadow 文字阴影
8. box-shadow 盒阴影
9. @media() 媒体查询，定义多套css，当浏览器的尺寸变化时，会采用不同的属性，主要用于自适应的时候

### 3. 请解释一下CSS3的 flexbox(弹性盒布局模型),以及适用场景？
该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。
在传统的布局方式中
- block 布局，是把块在垂直方向从上到下依次排列
- inline布局，在水平方向从左到右排列
- float布局，是在垂直方向的水平方向上从左到右，或者从右到左排列，宽度不够，就自动换行。
- flex布局，既可以水平也可以垂直，相对自由很多。

适用场景：
- 移动前端开发，在安卓和ios完美支持
- IE9+的浏览器
- 水平垂直居中非常方便！

# 参考资料

- [50道CSS基础面试题——（segmentfault：刘宁Leo）](https://segmentfault.com/a/1190000013325778)

# BFC规范了解一下
<!-- TOC -->

- [BFC规范了解一下](#bfc规范了解一下)
      - [什么是BFC？](#什么是bfc)
        - [box：css布局的基本单位](#boxcss布局的基本单位)
        - [formatting context:一个决定如何渲染文档的容器](#formatting-context一个决定如何渲染文档的容器)
      - [如何触发BFC？](#如何触发bfc)
      - [BFC的作用](#bfc的作用)
- [参考资料](#参考资料)

<!-- /TOC -->

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
满足以下条件之一的就可触发BFC（:question:还是没懂。。。。）

  - 根元素，即html;
  - float的值不为none;
  - overflow的值不为visible
  - display的值为block,list-item,table，inline-block，table-cell，table-caption，flex或inline-flex；
  - position的值为absolute或fixed

#### BFC的作用
1. 利用BFC避免margin重叠
2. 自适应两栏布局
3. 清楚float

总结：
因为BFC内部的元素和外部的元素绝对不会互相影响。因此，当BFC外部存在浮动时，它不应该影响BFC内部的布局，BFC会通过变窄，而不与浮动有重叠；
同样，当BFC内部有浮动时，为了不影响外部元素的布局，BFC计算高度时会包括浮动的高度。避免margin重叠也是同样道理。

# 参考资料
- [什么是BFC？看这一篇就够了——（CSDN：Leon_94）](https://blog.csdn.net/sinat_36422236/article/details/88763187)
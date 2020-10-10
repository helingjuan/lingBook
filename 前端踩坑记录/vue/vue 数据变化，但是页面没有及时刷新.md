---
title: vue 数据变化，但是页面没有及时刷新
tags: vue
notebook:
---
# vue 数据变化，但是页面没有及时刷新
——用强制渲染`this.$forceUpdate()`
### 原因分析
造成这种情况的可能原因：
- 数据层次太多，render函数没有自动更新，需手动强制刷新
- 代码问题



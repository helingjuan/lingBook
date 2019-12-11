---
title: elementUI的表格使用踩过的坑
tags: elementUI
notebook: 前端
---
# elementUI的表格使用踩过的坑
这里记录使用表格时，踩过的坑，给我注意点！

## 多表格时key必须要！且参数要不同
在一个页面有多个表格的时候，初始化进来是正常的，但是切换到另一个表格，再切换回来，表格数据就错乱了。参数对应不上。
就像这样：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191211160724.png)

### 解决方法：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191211161025.png)

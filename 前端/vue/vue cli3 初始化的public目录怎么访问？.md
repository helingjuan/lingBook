---
title: vue cli3 初始化的public目录怎么访问？
tags: vue
notebook: 前端
---
# vue cli3 初始化的public目录怎么访问？
## Q1：public里要放什么？
用vue cli 3.X版本初始化的项目根目录下面，有和src同级的public目录。

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191230155018.png)

> 官网的说明是说：用来放图片的，这样不管是打包还是dev起服务的时候，都可以通过根目录进行访问。

所以适合于放一些**需要在根目录访问的文件**。

## Q2:public根目录要怎么访问？
比如在public里建了一个文件夹img，里面放了一个logo.png 。
这时候某个页面要使用这张图片，那我们该怎么引入？？？
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191230155125.png)

### 解决方法

设置 publicPath 路径`publicPath: process.env.BASE_URL`，然后直接引用`${publicPath}`

举个例子：

``` vue
<template>
  <div class="er">
    <el-scrollbar style="height:100%">
      <div class="ds">
        <img class="sdde" :src='`${publicPath}img/logo.png`'>
      </div>
    </el-scrollbar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      publicPath: process.env.BASE_URL
    }
  }
}
</script>
```

## 参考资料
- [vue@cli3 项目模板怎么使用public目录下的静态文件,找了好久都不对，郁闷！(博客园-爱吃巧克力的狗)](https://www.cnblogs.com/wzcsqaws/p/11283228.html)






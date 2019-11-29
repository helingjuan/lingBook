---
title: 用github做图床，简单好用！
tags: 记录
notebook: 记录
---
# 用github做图床
因为初衷是写笔记的时候，可以浏览即可，要求不高，所以github正合适，原因是：免费且加载速度可以接受。
来看看是怎么做的吧。

### 一.建一个仓库
首先，你应该有一个github账号，然后创建一个仓库即可。(仓库名称自定义)  
**步骤**：
![image](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%2035.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%2036.png)

### 二.上传文件到仓库
这里有2种方式，1. 拖拽方式直接上传；
2.用git方式上传。

1. 拖拽方式
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826154634.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826154657.png)

2. git方式
   就是命令行
   ```
   git add --all .
   git commit -am "remark"
   git pull
   git push
   ```



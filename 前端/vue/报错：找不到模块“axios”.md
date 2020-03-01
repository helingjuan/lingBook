# 报错：找不到模块“axios”
<!-- TOC -->

- [报错：找不到模块“axios”](#%e6%8a%a5%e9%94%99%e6%89%be%e4%b8%8d%e5%88%b0%e6%a8%a1%e5%9d%97axios)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [分析](#%e5%88%86%e6%9e%90)

<!-- /TOC -->
 ## 概述
```node
import axios from 'axios'
```
  在我们引用axios的时候，报错，“找不到axios”
 这是为什么呢？

 ## 分析
 这是因为你的依赖中没有axios，去安装一下就好了！
 ```node
 npm i axios -S
 ```
 
---
title: markdownTOC不换行
tag: markdown
notebook: markdown
---

# markdownTOC不换行
<!-- TOC -->

- [markdownTOC不换行](#markdowntoc%e4%b8%8d%e6%8d%a2%e8%a1%8c)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [解决方法](#%e8%a7%a3%e5%86%b3%e6%96%b9%e6%b3%95)
    - [方法1：在图文界面里直接修改](#%e6%96%b9%e6%b3%951%e5%9c%a8%e5%9b%be%e6%96%87%e7%95%8c%e9%9d%a2%e9%87%8c%e7%9b%b4%e6%8e%a5%e4%bf%ae%e6%94%b9)
    - [方法2：在setting.json页面里直接改](#%e6%96%b9%e6%b3%952%e5%9c%a8settingjson%e9%a1%b5%e9%9d%a2%e9%87%8c%e7%9b%b4%e6%8e%a5%e6%94%b9)

<!-- /TOC -->
## 概述

在安装了插件`markdownTOC`之后，重启就可以看到鼠标右键会出来
就像这样
![例子](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%204.png)

```markdown

<!-- TOC -->1. autoauto[markdownTOC不换行](#markdowntoc%e4%b8%8d%e6%8d%a2%e8%a1%8c)autoauto -测试<!-- /TOC -->

```

而正确的是这样的

```markdown

<!-- TOC -->

- [markdownTOC不换行](#markdowntoc%e4%b8%8d%e6%8d%a2%e8%a1%8c)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [解决方法](#%e8%a7%a3%e5%86%b3%e6%96%b9%e6%b3%95)
    - [方法1：在图文界面里直接修改](#%e6%96%b9%e6%b3%951%e5%9c%a8%e5%9b%be%e6%96%87%e7%95%8c%e9%9d%a2%e9%87%8c%e7%9b%b4%e6%8e%a5%e4%bf%ae%e6%94%b9)
    - [方法2：在setting.json页面里直接改](#%e6%96%b9%e6%b3%952%e5%9c%a8settingjson%e9%a1%b5%e9%9d%a2%e9%87%8c%e7%9b%b4%e6%8e%a5%e6%94%b9)

<!-- /TOC -->
```

## 解决方法

### 方法1：在图文界面里直接修改

在文件-首选项-设置里，搜索eol ,把files的设置从`auto` 改为`\n`即可。

### 方法2：在setting.json页面里直接改

添加下面这句配置即可。

```json

"files.eol": "\n"

```

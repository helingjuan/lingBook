# 如何系统重装-win10系统
<!-- TOC -->

- [如何系统重装-win10系统](#如何系统重装-win10系统)
  - [1.概述](#1概述)
  - [2.工具准备](#2工具准备)
    - [MediaCreationTool1909的用途](#mediacreationtool1909的用途)
  - [3，制作u盘启动盘](#3制作u盘启动盘)
    - [3.1 运行MediaCreationTool1909.exe，选择`为另一台电脑创建安装介质`](#31-运行mediacreationtool1909exe选择为另一台电脑创建安装介质)
    - [3.2 再选择语言等。](#32-再选择语言等)
    - [3.3 选择介质（U盘）](#33-选择介质u盘)
  - [4.重装系统](#4重装系统)
    - [4.1 进入系统的BIOS，启动方式改为U盘启动](#41-进入系统的bios启动方式改为u盘启动)
      - [常用电脑的快捷方式](#常用电脑的快捷方式)
    - [4.2 进入到了BIOS，选择你的U盘](#42-进入到了bios选择你的u盘)
    - [4.3 选择语言等](#43-选择语言等)
    - [4.4 选择`自定义:仅安装windows（高级)(C)` 的安装方式](#44-选择自定义仅安装windows高级c-的安装方式)
    - [4.4 接受许可条款](#44-接受许可条款)
    - [4.5 选择吧windows安装在哪里，一般是主分区的c盘](#45-选择吧windows安装在哪里一般是主分区的c盘)
  - [参考资料](#参考资料)

<!-- /TOC -->
## 1.概述

最近需要重装下电脑，就去研究了一波，这里主要是重装成win10的系统。
哦，忘了说，我要重装的系统本身就是win10的

## 2.工具准备

需要以下几个工具
1. 一个>=8G空的的U盘（一定要空的！）
   因为制作u盘启动盘会格式化u盘，所以建议一定要空的u盘
2. 一个window官方提供的工具`MediaCreationTool1909.exe`,
   可以点击这里下载工具[MediaCreationTool1909工具](https://www.microsoft.com/zh-cn/software-download/windows10),进去直接点击“立即下载工具”，就可以了。
   ![立即下载工具示例](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222-121212.png)

   这个非常好用，可以直接把u盘设置成系统启动盘，就可以不用去下载老毛桃啊那些再去制作启动盘，nice！

### MediaCreationTool1909的用途

有两种使用方式：

1. 直接把当前电脑升级成win10
2. 使用该工具创建安装介质(就是制作我们要的U盘启动盘)，以再其他电脑上安装win10(:point_left:就是我们要用到的)

其实具体怎么用，这个下载页面里都有相关介绍，但是为了方便！我们还是记录一下
准备好了，我们就要制作一个启动盘了。

## 3，制作u盘启动盘

### 3.1 运行MediaCreationTool1909.exe，选择`为另一台电脑创建安装介质`

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200220-234114.png)

### 3.2 再选择语言等。

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200220-234158.png)

### 3.3 选择介质（U盘）
然后就是等等等，等他安装好了（提示：“你的U盘已准备就绪”），就可以开始准备重装系统了
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200220-234216.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200220-234407.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200221-090741.png)

## 4.重装系统
### 4.1 进入系统的BIOS，启动方式改为U盘启动
就是在电脑logo出来的时候，立刻按下快捷键，进入BIOS(**!!!注意，是logo出来就立刻按**，因为不注意这个，不知道重启多少次电脑试图进入BIOS失败的过来人，建议你们不要尝试，会很心累:innocent:)

#### 常用电脑的快捷方式
- 华硕/ROG `ESC`
- 戴尔 `F12`
- 惠普 `F10`
- 联想/三星 `F2`

如果是其他牌子的，建议自己搜一下

### 4.2 进入到了BIOS，选择你的U盘
是的，没错，我就是金士顿2.0的，旧U盘，嘻嘻嘻
所以我就选`UEFI:KingstongDataTraveler 2.0PMAP`
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222124654.jpg)
### 4.3 选择语言等
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222124716.jpg)
### 4.4 选择`自定义:仅安装windows（高级)(C)` 的安装方式
### 4.4 接受许可条款
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222124721.jpg)

### 4.5 选择吧windows安装在哪里，一般是主分区的c盘
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222124729.jpg)

问我怎么看出来是c盘的？先看空间大小啊，然后就是直觉吧
然后就一直等了
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222124734.jpg)

等啊等
下一步啊下一步
重启啊重启
你就会看到windows激活页面了，然后激活它就可以了。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20200222124739.jpg)

完事！
over

等等，你问我怎么激活windows？
送你下一步大法（一直下一步）。

## 参考资料

- [MediaCreationTool1909工具下载](https://www.microsoft.com/zh-cn/software-download/windows10)
- [如何重装win 10 系统？(知乎-金源)](https://www.zhihu.com/question/54059979)
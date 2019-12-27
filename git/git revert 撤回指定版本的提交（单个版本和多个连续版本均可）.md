---
title: git revert 撤回指定版本的提交（单个版本和多个连续版本均可）
tags: git
notebook: git
---
# git revert 撤回指定版本的提交（单个版本和多个连续版本均可）
<!-- TOC -->

- [git revert 撤回指定版本的提交（单个版本和多个连续版本均可）](#git-revert-撤回指定版本的提交单个版本和多个连续版本均可)
  - [概述](#概述)
  - [1.撤回某个指定版本`git revert <commitId>`](#1撤回某个指定版本git-revert-commitid)
    - [撤回前](#撤回前)
    - [撤回后](#撤回后)
  - [2. 撤回连续多个版本，并合并成一个版本](#2-撤回连续多个版本并合并成一个版本)
    - [具体截图](#具体截图)
      - [1. 把要撤回的版本，一个个revert `git revert <commitId>`](#1-把要撤回的版本一个个revert-git-revert-commitid)
      - [2. 合并版本 `git rebase -i <commitId 所要合并到的版本id>`](#2-合并版本-git-rebase--i-commitid-所要合并到的版本id)
      - [3.修改文件](#3修改文件)
      - [4. 提交](#4-提交)
  - [3.拓展](#3拓展)
  - [参考资料](#参考资料)

<!-- /TOC -->
## 概述

因为一些操作，不小心把其他分支上的代码拉到主线上去，并提交了。为了即时止损，我们现在最快速的操作就是，撤回这些不小心被提交上去的版本。
大概有3种撤回方式：`git revert`,`git reset`, `git restore`
简单介绍一下：
- `git revert` 在撤销之前的版本的时候，会新建一个版本，并写上所撤销的版本信息（推荐！）
- `git reset` 直接把之前提交的版本删除，这个操作非常危险！谨慎使用
- `git restore` 取消暂存

提示：这里有个很关键的数据，commitId，就是所提交的版本号，要怎么知道呢？
有2种方式：
1. 通过命令`git log`查看；
  举个例子：
  ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227163242.png)
2. 在仓库那里，点击提交历史，就可以看到
 ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227163242.png)

这些都是有效的commitId
顺便说一下，进去后，要出来怎么办？（我一开始就被困住了）
—— 通过快捷键`Shift + Q`出来！！！ 救每个被困的人

## 1.撤回某个指定版本`git revert <commitId>`
```
git revert <commitId>
```
可以通过`git log`来查看版本的区别
### 撤回前
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227163242.png)
### 撤回后
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227163229.png)

如果在撤回的时候发现有问题（冲突什么的），就试试这样：
```
git revert <commit_id>
//如果commit_id是merge节点的话,-m是指定具体哪个提交点
git revert <commit_id> -m 1
//接着就是解决冲突
git add -all .
git commit -m "revert some"
git revert <commit_id> -m 2
//接着就是解决冲突
git add -all .
git commit -m "revert some"
git push
```
看看撤销成功后的效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227165105.png)

## 2. 撤回连续多个版本，并合并成一个版本
步骤：
1. 把要撤回的版本，一个个revert `git revert <commitId>`
2. 合并版本 `git rebase -i <commitId 所要合并到的版本id>`
3. 修改文件
4. 提交即可

### 具体截图
这部分主要参考[git revert + git rebase 一次性回退多个提交(CSDN-本然233)](https://blog.csdn.net/qq_35008279/article/details/86316819)
所以如果要看详细内容，可以移步这里，因为我在尝试的时候，有的步骤忘记截图了 哈哈哈哈
#### 1. 把要撤回的版本，一个个revert `git revert <commitId>`
```
git revert <commitId>
```
就是，一个一个一个一个合并
记得先git log 然后把自己确定要撤回的版本复制出来，然后就重复性操作啦
#### 2. 合并版本 `git rebase -i <commitId 所要合并到的版本id>`
```
git rebase -i <commitId 所要合并到的版本id>
// 这里我用的是最最最早要撤回的那个版本号
```
然后，它就会弹出一个编辑页，像这样
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/2019011120240327.png)
这就到我们第三步了。
#### 3.修改文件
因为我们要把多个提交合并到一个提交里去。就需要修改这个文件
**把pick 改成 s**
仔细看，文档里，也有说明具体每个关键字的意思。
p或pick 就是使用这个版本
s或squash，就是使用这个版本，但是合并到先前的版本中去。
最后，**保留一个pick，其他都改成s**

然后，我，我...又被困住了。。。这里我同样要救救被困住的人！（比如我）
看看**怎么保存并退出**！！
先`Ctrl + X` 退出， 然后它会提示你是否保存修改，你就`Y`确定，然后就出去了（好像，如果我没记错的话）
不要去按`Ctrl + O`修改文件这种辣鸡命令，会困到你只有关闭终端才能解脱（不要问我是怎么知道的）

好了，我们终于提交好了，然后就等他执行完命令，执行完，就又有一个文档跳出来了。
我的参考资料和我说，我要去修改一下提交的提示，但是！
我懒，太多了，就这样吧，就直接退出`Ctrl + X`
要不要改随你，这只是个commit提示而已。
#### 4. 提交
最后，终于终于可以提交了，
```
git push
```
看看撤销成功后的效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227165242.png)

## 3.拓展

git官方文档的示例中，是使用指针的方式进行撤回的。但是因为没有尝试过，所以就作为拓展吧。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191227162738.png)

## 参考资料
- [git revert 官方文档](https://git-scm.com/docs/git-revert)
- [git 优雅的撤销中间某次提交(CSDN-山鬼谣me)](https://blog.csdn.net/u013066244/article/details/79920012)
- [git revert + git rebase 一次性回退多个提交(CSDN-本然233)](https://blog.csdn.net/qq_35008279/article/details/86316819)


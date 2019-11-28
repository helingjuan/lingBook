---
title: git 常用命令记录
tags: git
notebook: git
---
# git 常用命令记录
先看看别人整理出来的图。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1533814345565.png)
### 一.克隆项目 clone
把远程仓库上的项目克隆到本地。一般来说项目是至少至少有1个或2个分支，主要是做开发和线上的区别。既然所属分支不一样，那命令也会有一点区别。*这里假设是有2个分支，dev 和master*
#### 1.1 常见的克隆（master分支）
```
//最常见的用法
git clone <仓库地址> // 一般默认克隆的是master分支
```
#### 1.2 克隆dev分支（或指定的一个分支）
```
// 1.dev分支
git clone -b dev
// -b 即使-branch 的缩写，就是指明dev分支。


// 2.指定的分支
git clone -b <分支名>
```

### 二.更新本地项目（拉取） pull
更新项目一般是远程仓库上的项目已经更新了，本地仓库需要**拉取**那个更新，把当前项目更新为最新状态。    
就是更新本地仓库   
这里又分为两种，只有一个分支的，和有多个分支的。   
#### 2.1 单分支(master)
```
git pull
```
#### 2.2 多分支，更新dev分支的
```
// 只更新dev分支
//方法1（亲测可用）
git pull origin dev

//方法2 （备用，网上看到的）
git fetch origin master
git log -p master.. origin/master
git merge origin/master
```

### 三.更新远程仓库的项目（推送-上传代码）push
#### 3.1 单分支(master)
```
git push
```
#### 3.2 多分支(比如：dev)
```
git push origin dev
语法：git push origin <branch>
```

### 四.关于分支的一些操作
#### 4.1 新建分支 branch
```
git branch 分支名，如dev
//语法：git branch <branchName>
```

#### 4.2 切换分支 checkout
```
git checkout 分支名，如dev
```

#### 4.3 查看该项目的分支数
```
//查看当前项目的所有分支数（本地+远程）
git branch -a 
//查看本地分支
git branch
//查看远程分支
git branch -r
```
#### 4.4 删除本地分支
```
//删除本地分支
git branch -D 分支名

```
#### 4.5 删除远程分支
```
git push origin --delete 分支名
```
### 五.查看本地项目对应的远程仓库地址 remote
```
git remote -v
// git remote ,查看当前配置有哪些远程仓库
```
#### 5.1 添加远程仓库地址 add
```
git remote add 指针名 仓库地址
```
#### 5.2 删除远程仓库地址 remove
```
git remote remove 远程地址
```
### 六.拉取远程另外一个仓库的代码 remote
```
// 建一个指针，指向远程的另外一个仓库
git remote add 指针名 仓库地址
// 然后查看本地的链接
git remote 
// 然后使用那个指针进行拉取
git pull 指针名 分支名

```
举例：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191016171804.png)


![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532342578342.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532342570031.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532342564849.png)

### *.其他
#### *.1 初始化项目 init
进入项目文件夹的根目录里，通过初始化该项目，让这个项目变成git可以管理的仓库。
```
git init
```

#### *.2把文件添加到版本库里
在提交文件之前，需要把所有的文件都先添加到暂存区里去。   
```
git add . 
//方法2
git add --all .
```
**注意：** 这里的点（.） 和前面的单词之间要隔一个空格。点的意思，就是添加这个文件夹下面的所有文件。

#### *.3 添加提交文件的备注说明
```
git commit -m "备注信息"
//方法2
git commit -am "备注信息"
```

#### *.4 关联到远程库
```
git remote add origin 远程仓库地址
比如：git remote add origin http://github.com/demo.git
```

### 参考资料:
- [如何用命令将本地项目上传到git——eedc(博客园)](https://www.cnblogs.com/eedc/p/6168430.html)
- [git fetch 更新远程代码到本地仓库——圣耀（博客园）](https://www.cnblogs.com/chenlogin/p/6592228.html)
- [git命令-远程仓库拉取、本地仓库更新、工作空间提交等等——jtracydy（CSDN）](https://blog.csdn.net/jtracydy/article/details/70402663)
- [git提交项目到已存在的远程分支——林七七（博客园）](https://www.cnblogs.com/JennyLin77/p/git.html)


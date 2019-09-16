---
title: git 安装及使用
tags: git
notebook: git
---
# git 安装及使用

### 一.下载
官方地址：https://git-scm.com/downloads 
1. 选择适合自己的版本，下载；
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image.png)
2. 下载完成后，是个exe文件，直接双击安装。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B1%5D.png)
### 二.安装
1. 选择安装路径：（自定义）
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B2%5D.png)
2. 选择组件
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B3%5D.png)
3. 选择默认git 的编辑器
 ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B4%5D.png)
4. 调整path环境
   就是用什么方式使用git命令行的。
   ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B5%5D.png)  
   标注1： 只使用git bash
   标注2：使用windows下的cmd
5. 选择ssh等等等。
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B6%5D.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B7%5D.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B8%5D.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B9%5D.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B10%5D.png)
6. 安装成功
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B11%5D.png)
### 三.初始化
#### 3.1 设置git全局变量（用户名，邮箱号）
```
// 用户名
git config --glocal user.name "heihuahe(用户名)"
// 邮箱
git config --glocal user.email "example@163.com(邮箱)"
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B12%5D.png)
#### 3.2 查看设置好的账号
```
git config --list
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B13%5D.png)
#### 3.3 新建仓库并初始化

```
// 方法1：纯命令行方式
mkdir testssm // 新建一个文件夹
cd testssm // 切换到这个testssm文件夹里
git init // 初始化
```
```
// 方法2：去到对应的文件夹，然后直接初始化
git init
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B14%5D.png)
然后查看生成的仓库。一般来说会生成一个.git的文件夹
若仓库内是空的，设置下显示隐藏的项目，就可以了   
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B15%5D.png)
#### 3.4 克隆项目
```
git clone 仓库地址
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B17%5D.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/Image%20%5B18%5D.png)
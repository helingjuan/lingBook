---
title: git 上传文件到仓库
tags: git
notebook: git
---
# git 上传文件到仓库

就是新建一个仓库，然后把已经写好了的代码或文件上传到这个仓库里。  
大概有这3种方法：
- 可视化操作-直接拖拽上传（适合文件数量较少的）
- 先初始化仓库，然后把**已有的代码文件**与这个仓库关联，然后上传。
- 先初始化仓库，直接克隆仓库，然后再在这个文件夹里直接操作。

### 方法1：直接拖拽上传
众所周知，方法一就直接拖拽了，没什么必要具体说明了，就，略过。

### 方法2：初始化-关联-上传
这里假设你已经在git里新建了一个仓库A了。  
下面你还需要执行7步操作：
1. 到对应的文件夹根目录里，右键，打开 `git bash`
2. 执行操作：`git init` 初始化这个文件夹
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532015584284.png)
3. 把文件夹里的文件都添加到版本里 `git add .`
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532015656179.png)  
*下面的提示，不管他，不影响*
4. 添加这个版本的备注：`git commit -m "版本备注"`
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532015743190.png)
5. 复制仓库A的地址
6. 关联远程仓库和本地仓库（画重点！）：`git remote all origin 仓库A地址`
7. 上传代码：`git push -u origin master`
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1532015958922.png)

### 方法3：初始化-克隆-上传
这里假设你已经在git里新建了一个仓库A了。   
下面你还需要执行5步操作：
1. 到你想存放的文件夹根目录，打开git bash
2. 克隆仓库A：'git clone 仓库A地址'
3. 然后`add-commit-push` 3步走   
   因为这是全新的仓库，我就省去了pull这一步了。
### 参考资料
- [两种方法上传本地文件到github
(简书-hanyuntao)](https://www.jianshu.com/p/c70ca3a02087)

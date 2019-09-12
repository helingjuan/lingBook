---
title: git 免密登录
tags: git
notebook: git
---
# git如何免密登录

### 一.http账号密码
去项目的文件夹下，打开隐藏文件夹.git    
找到config文件，右键打开     

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826155750.png)
然后就可以免密登录了，缺点就是麻烦，要一个个设置过去。
### 二.ssh登录
1. 生成ssh密钥    
   `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
2. 找到公钥id_rsa.pub,复制
3. 去git仓库下，新建ssh密钥    
  ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826153604.png)
  ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826120205.png)
  ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826154233.png)
4. 如果是更改已有的项目，就需要这步操作，直接克隆的就可以跳过
  ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826165223.png)
  ![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826165316.png)
5. 测试连接，即可    
   `ssh -T git@github.com(配置ssh密钥的仓库域名)` 或直接`git pull`    
   
完整流程：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826152638.png)

#### 看看配置好的ssh目录有哪些？
打开文件夹，或者用命令行的方式都行，
1. 命令行方式
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826160638.png)
2. 文件夹方式
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826160308.png)

说明： 
```
id_rsa  就是私钥文件
id_rsa.pub 就是我们这次要用的公钥文件
known_hosts 连接过的主机，里面会存这些主机域名的信息
```
**这个ssh连接的优点就是一步到位！**，后面再也不用考虑密码的问题了。就是一开始配置麻烦一点点。



### 遇到的问题：1.报错Permission denied (publickey,keyboard-interactive).
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826143926.png)
在测试连接的时候一直报**权限拒绝**的错误，就一直连接失败。    
后来找了好久，发现是我环境的问题。
因为我的环境是，执行`git add` 或者 `git pull` 等git命令，都要在最前面加 `sudo`, 然而我在生成ssh密钥的时候没有加`sudo`,这个就导致我的密钥权限不够。   

**生成ssh密钥的时候，一定要和平时的权限一致！！该加sudo就加sudo**
> `sudo`就是相当于执行超级管理员的权限。


### 遇到的问题：2.Enter passphrase for key '/c/Users/DELL/.ssh/id_rsa 是什么意思？
就是github账号的密码。    
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190826142354.png)



---
title: git 修改注释信息
tags: git
notebook: git 
---
# git 修改注释信息
### 1.修改还未push的注释 
```
git commit --amend
```
3步：  
1. 编辑器编辑：
   - vim 编辑器 ：修改后保存退出:wq （先按esc 退出，然后按：，输入wq 保存并退出）
    - xshell 不知道是什么的编辑器，找到writeOut （Ctrl + o），然后直接回车，就编辑成功了。
2. 然后选DOC模式 （M-A DOC format），输入M_A
3. 然后 回车 Yes
### 2.修改刚刚push到远程仓库的注释
#### 2.1 没被别人下载/改动过
3步：
1. 修改  `git commit --amend`
2. 保存后退出 `:wq`
3. 重新推上去 `git push --force-with-lease origin master`


#### 2.2 被别人下载/改动了的
2步：  
1. `git fetch origin`
2. `git reset --hard origin/master`


### 参考资料
- [git修改未push和已经push的注释信息 (CSDN - yulsh)](https://blog.csdn.net/yulsh/article/details/54613189)
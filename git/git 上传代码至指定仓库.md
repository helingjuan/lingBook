---
title: git 上传代码至指定仓库
tags: git
notebook: git
---
# git 上传代码至指定仓库
发现这个其实也是可以拓展很多情况的，就单独列出来吧。

常见方法（有3种）:
1. add 并且commit，再checkout，提交到当前分支；
2. add但不commit，可以stash，然后checkout回来之后stash apply ，再commit ，提交到当前分支
3. add ——checkout ——commit，提交记录就在切换分支下面。

### 方法1：add 并且commit，再checkout，提交到当前分支 
介绍：   
1. 在对应的文件夹根目录打开git bash 界面
2. 将索要提交的文件信息（修改过和更新过的文件）添加到索引库`git add --all . `    
3. 根据索引库的内容进行文件提交 `git commit -m "描述信息"`
4. （如果已存在分支可以跳过这步）新建分支 git branch 分支名，如dev
5. 查看该项目的所有分支(本地和远程)，并在当前所在分支前加*标记。`git branch -a`
    - 只查看本地分支 `git branch`
    - 只查看远程分支 `git branch -r`


6. 切换本地分支 `git checkout <branch>`，如dev   
  
7. 将远程分支的代码pull到本地分支 `git pull origin dev:dev`
`git pull <远程主机名> <远程分支名>:<本地分支名>`
8. 把本地分支的代码推到远程分支中`git push origin dev:dev`
`git push <远程主机名> <本地分支名>:<远程分支名>`


### 提交dev分支，并用dev分支的内容覆盖master分支
提交dev后，要把master 的也提交

1. 切换分支到master `git checkout master`
2. 查看当前分支，确认下是否切换成功了 `git branch`
3. 拉取master分支内容 `git pull origin master`
4. 把dev的覆盖mster分支 `git merge dev(这样就可以不用重复add commit 了)`
5. 更新 `git push origin master`
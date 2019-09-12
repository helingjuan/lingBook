---
title: git 版本回滚 
tags: git
notebook: git
---
# git 版本回滚
有时候啊，突发情况，就需要版本会滚，还是记录一下，不能生疏！
### 回滚到指定的版本
3步：
1. 查看最近提交的版本记录 `git log`
2. 回滚到指定的版本
   ```
   git reset --hard 版本的commit值，如
   git reset --hard 26702460a5acf87a61373f10a58dfccf9a453e4a
   ```
3. 强制提交 `git push -f origin master`  
    
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552298907757.png)
### 回滚到上一个版本（删除最新的版本）
```
// 1.
git revert HEAD
// 2.
git push origin master// 分支名
```
> `revert：` 放弃指定提交的修改，但是会生成一次新的提交，需要填写提交注释，以前的历史记录都在；
`reset：` 将HEAD指针指到指定提交，历史记录中不会出现放弃的提交记录。
revert效果：   
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552896818319.png)
reset效果：（直接回滚到上一次的提交）  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552896863965.png)
### 参考资料
- [git回滚到任意版本 (博客园 - 知行合一)](https://www.cnblogs.com/wancy86/p/5848024.html)

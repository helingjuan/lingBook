---
title: git 报错Host key verification failed
tags: git
notebook:  git
---
# git 报错Host key verification failed
报错信息：
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
f8:00:24:39:fc:46:16:3f:09:ff:f4:11:fa:8c:bd:d6.
Please contact your system administrator.
Add correct host key in /root/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /root/.ssh/known_hosts:1
  remove with: ssh-keygen -f "/root/.ssh/known_hosts" -R src.nuguo.cn
ECDSA host key for src.nuguo.cn has changed and you have requested strict checking.
Host key verification failed.
fatal: Could not read from remote repository.
```
看了之后，感觉主要就是这句话：`ECDSA host key for src.nuguo.cn has changed and you have requested strict checking.
Host key verification failed.`
> 一般来说，这个问题就是重置服务器后，然后再次访问会出现的。  
> ——度娘说
#### 解决办法
是我的ssh密钥的权限问题，我这里要求是root用户的ssh密钥

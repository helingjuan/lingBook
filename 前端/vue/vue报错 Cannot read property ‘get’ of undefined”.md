---
title: vue报错 Cannot read property ‘get’ of undefined”
tags:
notebook:
---
# vue报错 Cannot read property ‘get’ of undefined”

## 完整报错信息
[Vue warn]: Error in mounted hook: “TypeError: Cannot read property ‘get’ of undefined”


这个是什么问题啊
this?
axios 获取到的数据，没有在this中成功赋值。

啊啊啊啊啊 **是created 和mounted 的问题**。辣鸡

**记住：mounted 不一定就是晚于created 执行，他们有可能是同步执行的。**



---
title: 移动端没有:hover事件
tags: 
notebook: 
---

### 判断是pc端还是移动端
```
// 判断是pc还是移动
function isMobile() {
  // 移动端
  if ((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    return true
 }else{ //pc端
    return false
}
}
```

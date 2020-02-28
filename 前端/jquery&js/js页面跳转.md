---
title: js页面跳转
tags: js
notebook: 前端
---
# js页面跳转
<!-- TOC -->

- [js页面跳转](#js%e9%a1%b5%e9%9d%a2%e8%b7%b3%e8%bd%ac)
    - [常用方法 location](#%e5%b8%b8%e7%94%a8%e6%96%b9%e6%b3%95-location)

<!-- /TOC -->
场景：经常在接口返回正确信息的时候，回到列表页或者其他，这时候通常是用js来控制的。

### 常用方法 location
```
//方法1：location.hash
location.hash = 'member/sportsTeamManage/sportsTeamList'

// 方法2：location.href
// path.t 是封装好的参数，带域名
location.href = path.t('member/sportsTeamManage/sportsTeamList')
```


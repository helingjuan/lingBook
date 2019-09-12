---
title: js页面跳转
tags: js
notebook: 前端
---
# js页面跳转

场景：经常在接口返回正确信息的时候，回到列表页或者其他，这时候通常是用js来控制的。

### 常用方法 location
```
//方法1：location.hash
location.hash = 'member/sportsTeamManage/sportsTeamList'

// 方法2：location.href
// path.t 是封装好的参数，带域名
location.href = path.t('member/sportsTeamManage/sportsTeamList')
```


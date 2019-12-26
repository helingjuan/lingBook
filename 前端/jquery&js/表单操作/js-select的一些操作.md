---
title: js-select 的一些操作
tags: js
notebook: 前端
---

# js-select的一些操作

### 筛选项数据由后台返回
```
// 方法1：appendTo
var list = data.list;
$("<option value=''>全部套餐</option>").appendTo($("#package_id"));
for (var k in list) {
    $("<option value='" + list[k].package_id + "'>" + list[k].package_name + "</option>").appendTo($("#package_id"));
}
```

```
//方法2： array push append

var tempArray = [];
tempArray.push('<option value="">全部推荐人</option>')
for(var i in res.list) {
  var name = res.list[i].user_realname? res.list[i].user_realname: res.list[i].user_name
  tempArray.push('<option value="'+res.list[i].adm_id+'">'+name+'</option>')
}
$("#introducer").append(tempArray.join('')).select2()

```


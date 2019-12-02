---
title: checkbox的一些操作，全选
tags: js
notebook: 前端
---

# checkbox的一些操作，全选
### 发现checkbox checked属性问题（敲重点！）
就是在html中，**只要有checked这个属性，不管值是多少，空、true、false等，其效果都是选中的。**
所以要操作这个，只能从js来判断。   
举例：    
```
```
效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190829144856.png)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190829144915.png)

### js||jQuery 选中某复选框
```
//方法一：js
document.getElementById("genderMan").check = true
// 方法二：jQuery-attr
$("#genderMan").attr("checked", true)
// 方法三：jQuery-prop
$("#genderMan").prop("checked", true)
```
举例：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190829150435.png)

拓展：**attr和prop有什么区别？**
> 自 jQuery 1.6 版本起，attr() 方法对于未设置的 attributes （即标签中没写该 attributes）都会返回 undefined。对于检索和改变 DOM 的 properties，如表单元素的 checked、selected 或 disabled 状态，应使用 .prop() 方法。


### 获取选中的复选框的值


### 列表的全选
```
// html
// 表头
<tr>
    <th style="width:8px;" class="sorting_disabled">
        <input type="checkbox" class="group-checkable" onclick="mm.selectAll(this)"/>
    </th>
    <th class="auto-line text-center">会员卡号</th>
    <th class="auto-line text-center">物理卡号</th>
    <th class="auto-line text-center">创建时间</th>
    <th class="auto-line text-center">状态</th>
    <th class="auto-line text-center">激活场馆</th>
    <th class="auto-line text-center">激活日期</th>
    <th class="auto-line text-center">操作</th>
</tr>
// 列表项中的checkbox
<td class="auto-line">
  {{#condition is_checked '==' false}}
  <input class="check" name="checkbox" type="checkbox">
  {{/condition}}
  {{#condition is_checked '==' true}}
  <input class="check" name="checkbox" type="checkbox" checked>
  {{/condition}}
</td>
```
```
// jquery  敲重点
mm.selectAll = function(tag) {
    $("input[type='checkbox']").prop('checked', $(tag).prop('checked'))
  }
```
效果：    
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/checkbox-selectAll.gif)

### 判断复选框是否被勾起了
```
$("#is_menu_checked_all").checked // true就是勾起了，false就是没有
```
```
/**
     * 权限全选
     */
    $("#is_menu_checked_all").click(function() {
      if((this).checked) {
        $("input[type='checkbox']").prop('checked', true)
      } else {
        $("input[type='checkbox']").prop('checked', false)
      }
    })
```
### 参考资料
- [复选框之checked属性(博客园-江峰)](https://www.cnblogs.com/jf-67/p/6613898.html)
- [jQuery 的 attr 与 prop 的区别(github-JChehe)](https://github.com/JChehe/blog/blob/master/posts/jQuery%20%E7%9A%84%20attr%20%E4%B8%8E%20prop%20%E7%9A%84%E5%8C%BA%E5%88%AB.md)

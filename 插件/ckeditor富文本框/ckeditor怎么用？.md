---
title: CKEditor 怎么用？
tags: 富文本框
notebook: 前端
---

# CKEditor 怎么用？

### 引入插件
主要是 ckeditor.js 和 config.js文件
config是这个富文本框的通用配置文件，如果有什么新需求，直接去那里加就好。
举例：    
```
$view->addJsReload('page.js',array(__PUBLIC__.'/ckeditor/ckeditor.js',__PUBLIC__.'/ckeditor/config.js'));
```
### html页面
用`textarea`就可以，
举例：
```
<textarea id="remark"  style="width:800px;height:400px;" name="remark"></textarea>
```
### js初始化
```
// 富文本编辑器 ckeditor 初始化
var editor = CKEDITOR.replace('remark', {
  height: '400',
  width: '700',     
})
```

### 修改富文本框内容后，回显必备之更新实例
```
// 更新实例
    function CKupdate() {
        for (instance in CKEDITOR.instances)
            CKEDITOR.instances[instance].updateElement();
    }
```

### 设置富文本框数据
```
// ckeditor 回显数据
editor.setData(data.option_value)
```

### 获取富文本框的数据
```
actDes = editor.getData();
```


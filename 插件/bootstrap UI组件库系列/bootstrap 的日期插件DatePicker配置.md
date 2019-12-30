---
title: bootstrap 的日期插件DatePicker配置
tags:
notebook:
---
# bootstrap 的日期插件DatePicker配置
## 依赖包：
bootstrap-datepicker.js
bootstrap-datepicker.css
bootstrap-datepicker.zh-CN.js //汉化包

## 配置
### 1.控制日期可选范围
- startDate ： 最小日期
- endDate： 最大日期
### 2.清除按钮 `clearBtn`
默认为false，不显示
```
clearBtn: true //显示清除按钮
```

举个例子：
```
$(“.datepicker”).datepicker({
language: “zh-CN”,
autoclose: true, //选中之后自动隐藏日期选择框
startDate: new Date(), //起始时间为今天
format: “yyyy-mm-dd”, // 日期格式
weekStart: 0,
todayBtn: true, // 今天按钮
});
```

## 参考资料
- [bootstrap-datepicker 官网](https://bootstrap-datepicker.readthedocs.io/en/latest/options.html)
- [Bootstrap-datepicker3官方文档中文翻译—Options/选项(博客园-tincyho)](https://www.cnblogs.com/tincyho/p/7978483.html)



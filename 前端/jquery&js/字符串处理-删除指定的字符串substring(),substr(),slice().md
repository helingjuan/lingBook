---
title: 字符串处理-删除指定的字符串substring(),substr(),slice()
tags: js
notebook: 前端
---
# 字符串处理-删除指定的字符串substring(),substr(),slice()
### substring()
——适合取字符串一段连续的部分，比如前半部分，后半部分，中间某段（明确具体的坐标）
- `substring(indexStart, indexEnd)`  
  返回在开始坐标(start index) 到截止坐标(end index)的那部分字符串，**(不包含截止坐标的那个字符)**
- `substring(indexStart)`  
  返回从起始坐标(indexStart)开始到字符串末尾的字符串   

*注意：*如果indexStart == indexEnd ,substring() 返回的就是一个空字符串。
如果indexStart > indexEnd ,substring()的执行结果就像两个参数调换了一样，就像`substring(indexEnd, indexStart)`

### slice()
与substring很像，也是需要明确的坐标
### substr()
`substr()`也是用于取一段连续的字符串，这个和substring有细微的区别，所以要仔细区别他们，避免混淆。
- `substr(indexStart, length)`   
取从indexStart开始到指定长度的那截字符串。

### 这三个的区别
- 相同点： 不用多说，就是截取字符串；
- 不同点：
  - substring()和slice() 其实很像，都是需要知道明确起止坐标，indexStart 和indexEnd
  - substr() 只需要知道起始坐标indexStart 和所要截取的长度即可，不关注终点坐标。
### 参考资料
- [String.prototype.substring()(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substring)
- [String.prototype.substring()(MDN文档-英文版)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)



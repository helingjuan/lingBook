---
title: js 金额数据处理math.round()
tags: js
notebook: 前端
---
# js 金额数据处理math.round()
## 概述
就是各种情况的金额数据处理
## 1. 四舍五入，且保留2位小数，且每3位用逗号分割
比如： 123456789.9546214
处理结果：123,456,789.95

```
// 保留小数点后面x位数 num  默认2位小数,且用逗号分割
mm.setPointByNum = function(num, pointNum) {
  var percent = 1;
  var point = pointNum || 2
  for (var i = 0; i< point; i++) {
    percent = percent*10
  }
  var numFloat = Math.round(num*percent)/percent
  var numStr = numFloat.toString()
  var index = numStr.indexOf('.')
  if (index < 0) {
    index = numStr.length;
    numStr += '.'
  }
  while (numStr.length <= index +point) {
    numStr += '0';
  }
  // 加逗号
  var numArrayStart = numStr.substring(0, index).split('').reverse(),
      numStrEnd = numStr.substring(index),
      numStrStart = '',
      result = '';
  for (var k in numArrayStart) {
    if (numArrayStart.length % 3 != 0) {
      numStrStart += numArrayStart[k] + ((k+1)% 3 == 0 && (k+1) != numArrayStart.length ? ',': '')
    }else {
      numStrStart += numArrayStart[k]
    }
  }
  result = numStrStart.split('').reverse().join('') + numStrEnd
  return result;
}
```
这个有bug
对负数没有做处理，比如 -169 就会变成-,169这样是不对的。
还有如果输入的数字式1,000 进去转换，就会报错，要去除掉这些字符,

**最后代码**
```
priceFormat(price, pointNum) { // 金额格式，保留两位小数，且用逗号分割，比如1，000.00
    let percent = 1
    let priceFloat = 1.0
    let priceStr = ''
    let pointIndex = 0
    let priceArrayInt = []  // 整数部分的数组
    let priceStrPoint = '' // 小数部分
    let priceStrInt = ''  // 整数部分
    const regNum = /^\d+$/ // 非负整数
    const point = pointNum || 2 // 默认2位小数
    for (let i = 0; i < point; i++) {
      percent = percent * 10
    }
    debugger
    priceFloat = Math.round(price * percent) / percent
    priceStr = priceFloat.toString()
    pointIndex = priceStr.indexOf('.')
    // 没有小数点的话，加小数点
    if (pointIndex < 0) {
      pointIndex = priceStr.length
      priceStr += '.'
    }
    // 位数不足，补0
    while (priceStr.length <= (pointIndex + point)) {
      priceStr += '0'
    }
    // 对整数部分处理，每3位加逗号
    priceArrayInt = priceStr.substring(0, pointIndex).split('').reverse()
    priceStrPoint = priceStr.substring(pointIndex)
    // 剔除掉整数前面的符号，比如-
    // 如果正好是3的倍数，就不用在前面加逗号
    for (const k in priceArrayInt) {
      // 不是3的倍数
      if (priceArrayInt.length % 3 !== 0) {
        // 去掉数据前面符号的影响
        // 最后一位是符号, 不算
        if (!regNum.test(priceStr.substring(0, pointIndex))) { // 负整数
          priceStrInt += priceArrayInt[k] + ((k + 1) % 3 === 0 && (k + 2) !== priceArrayInt.length ? ',' : '')
        } else { // 正整数
          priceStrInt += priceArrayInt[k] + ((k + 1) % 3 === 0 && (k + 1) !== priceArrayInt.length ? ',' : '')
        }
        // priceStrInt += priceArrayInt[k] + ((k + 1) % 3 === 0 && (k + 1) !== priceArrayInt.length ? ',' : '')
      } else {
        priceStrInt += priceArrayInt[k]
      }
    }
    return priceStrInt.split('').reverse().join('') + priceStrPoint
  },
```



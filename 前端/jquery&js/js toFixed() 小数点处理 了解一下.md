---
title: js toFixed() 小数点处理 了解一下
tags: js
notebook: 前端
---
# js toFixed() 小数点处理 了解一下
## toFixed([digits])文档介绍
- toFixed() 用指定的数字(digits)来格式化数字，比如: tofixed(2)， 就是会有2位小数。3 就是3位小数
- 参数：digits ，控制小数位数。2 就是2位小数，3 就是3位小数。这个数值范围在0-20之间。如果没传，则digits默认为0
- 返回值： 返回的是一个字符串。

举个例子：

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552291748107.png)

可以发现，**最后一个2.55 的结果是错误的。正确应该是2.6**

## toFixed() 的取舍规则是什么？
查了些资料，发现**toFixed() 的规则不是四舍五入，也不是 四舍六入五成双**

> 什么是四舍六入五成双？
> ——就是
> - 当<= 4 时，舍去；
> - = 6 时， 向上+1；
> - =5 时，由5后面的数字来决定，
>   - 当5后有数时，向上+1；
>   - 当5后没有数字时，看5前面的数字，
>     - 前面的那个数是奇数：向上+1；
>     - 前面的数字为偶数，舍5不进。

但是这个并不能覆盖所有情况，所以也pass

其实我们**困难点**很明确了，就是**当末尾是5的时候，不同浏览器给出的结果都不太一样**。这就会造成数据的偏差。如果是金融系统的话，那是非常致命的。

究其根本，是**浮点数的计算问题**，但是这个问题的规避不了得，
### 什么是浮点数计算问题？
比如 0.1 + 0.2 == 0.3 的结果就是false。这就是浮点数计算的问题。

在计算机中，所有的数值都是以二进制形式存放，比如2 ，就是010 ，0.1 就是 0.00011001…无限循环小数， 所以，**整数的计算一般不会出现误差，但是小数就会些误差。**

## 3种解决方法
1. **重写toFixed() 方法**
2. 在处理数据时，不要用toFixed() ,用Math.round() 但是这是专门处理整数的，所以要**先把小数变成整数**。他的取舍规则就是我们想要的四舍五入
3. toFixed() 和Math.round() 结合起来使用，**先四舍五入，再取小数点位数。**(:+1:推荐)

### 1.方法1： 重写
```
// 重写toFixed()
function overWriteToFixed() {
  Number.prototype.toFixed = function(d) {
    var s = this + '';
    if (!d) d = 0;
    if (s.indexOf('.') == -1 ) s += '.';
    s += new Array(d+1).join('0');
    if (new RegExp("^(-|\\+)?(\\d+(\\.\\d{0,"+(d+1)+"})?)\\d*$").test(s)) {
      var s = '0'+ RegExp.$2,
      pm = RegExp.$1,
      a = RegExp.$3.length,
      b = true;
      if (a == d+2) {
        a = s.match(/\d/g);
        if (parseInt(a[a.length - 1]) > 4) {
          for (var i = a.length -2; i>= 0; i--) {
            a[i] = parseInt(a[i]) +1;
            if (a[i] == 10) {
              a[i] = 0;
              b = i!= 1;
            } else break;

          }
        }
        s = a.join('').replace(new RegExp("(\\d+)(\\d{"+d+"})\\d$"),"$1.$2");
      }
      if (b) s= s.substr(1);
      return (pm+s).replace(/\.$/, '')
    }
    return this+''
  }
}
```
效果：

![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/.1552294576257.png)
### 3. 方法3 : toFixed() + Math.round()(:+1:推荐)
就是把小数变成整数，然后用`Math.round()`进行四舍五入，再除以那个倍数（小数变成整数的那个倍数），还原成小数，然后再使用toFixed(),取2位小数。

这样就不存在要通过toFixed()来四舍五入的情况了。

```
方法3 : toFixed() + Math.round()
// 计算，在一定额度内的手续费，取2位小数
// interest 是利率， allow_sum 额度范围内的数字， money 我要存的数字。
var value = (Math.round((money-allow_sum)*interest*100)/100).toFixed(2)
```

## 参考资料
- [文档 Number.prototype.toFiexed() (MDN文档)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)
- [JS中toFixed()方法的问题及解决方案 (博客园-柄棋先生)](https://www.cnblogs.com/wangsaiming/p/4644790.html)
- [十进制的0.1 为什么不能用二进制很好的表示？ (博客园-Company)](https://www.cnblogs.com/fandong90/p/5397260.html)
- [jquery的toFixed方法的正确使用 (博客园- 思心思危)](https://www.cnblogs.com/zengguowang/p/5981626.html)






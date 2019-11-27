---
title: 键盘事件介绍 KeyboardEvent
tags: webAPI
notebook: 前端
---
# 键盘事件介绍 KeyboardEvent
## 概述
KeyboardEvent对象描述了键盘的交互方式，有这么3种事件类型：`keydown`，`keypress`，`keyup`  
这些都是表示刚刚发生在键盘上的事件。所以**如果是用手机或者平板操作的话，就不会触发这个键盘事件**。   
其父对象是 UIEvent和Event，所以在方法和属性上，都会继承父对象的属性和方法。
## 1. 方法
`KeyboardEvent.getModifierState()` 返回一个Boolean，表示在事件创建时，修改键（比如：Alt、Shift、Ctrl等）是否按下

## 2. 属性
- `KeyboardEvent.altKey` 返回一个Boolean，判断是否按了按键`Alt`
- `KeyboardEvent.ctrlKey` 返回一个Boolean，判断是否按了按键`Ctrl`
- `KeyboardEvent.shiftKey` 返回一个Boolean，判断是否按了按键`Shift`
- `KeyboardEvent.metaKey` 返回一个Boolean，判断是否按了按键`Meta`,（meta 在Mac上是 `Command`,在windows上是win键）
- `KeyboardEvent.key` :+1:返回键值的DOMString，就是字符串
- `KeyboardEvent.code` 返回一个用事件表示值得DOMString
- `KeyboardEvent.charCode`:-1:**(不推荐使用，以后会废弃的属性)**  
  返回一个表示按键的Unicode编码的数字。且**这个属性仅由`keypress`事件使用**，如果有多个按键，就是返回第一个字符的Unicode编码值。  
  :exclamation:注意：在火狐里，这个属性会返回可打印字符的代码；
  （建议使用，`KeyboardEvent.key`代替！）
- `KeyboardEvent.keyCode`:-1:
  返回一个表示系统和实现相关数字代码的Number，用于标示按键的未修改值。
  （建议使用，`KeyboardEvent.key`代替！）
- `KeyboardEvent.which` :-1:返回一个表示系统和实现相关的数字代码Number，用于标识按键的未修改只，**通常来说，与`keyCode`值相同**
  （建议使用，`KeyboardEvent.key`代替！）
- `KeyboardEvent.locale` 返回一个表示区域的DOMString。如果浏览器或设备不知道，就可能为空字符串。
- `KeyboardEvent.location` 返回一个表示键盘或其他输入设备商按键位置的Number

## 3. 事件
关于那3个事件，文档是这么定义的。
- 当按钮被按下，触发`keydown`事件
- 如果这个按钮不是修饰键（Alt，Ctrl，Shift等）的话，就触发`keypress`事件
- 当按钮被释放，触发`keyup`事件

也就是说，一个按钮从按下到松开的过程中，事件是这么触发的：    
非修饰键：**`keydown` -> `keypress` -> `keyup`**   
修饰键：**`keydown` -> `keyup`**
### 3.1 特殊按键（可以切换指示灯状态的按键）
就是说那些可以切换指示灯状态的按键，比如Caps Lock键（大写锁定），Num Lock键（数码锁定），Scroll Lock键（滚动锁定）等。
:exclamation: 这些按键在windows和Linux上，仅触发`keydown`和`keyup`事件，而在mac上只触发`keydown`事件。

### 3.2 特殊情况（重复）
**当按键被按下，并被按住时（不松开），就会开始自动重复。这时候，事件就会重复被触发**，像这样：
1. keydown
2. keypress
3. keydown
4. keypress
5. ...(重复上1-2的过程)
6. 直到松开按钮，触发keyup

如果没看到这个，我会以为只会触发2次事件，就是1-2的过程，然后就是等松开按键，再触发keyup。所以还是注意一下吧！！！

### 3.3 监听事件
通常来说，我们想要知道键盘事件的时候，都是我们需要监控这个键盘，那么怎么监听键盘的事件就很重要了，我在查阅资料的时候，发现，大多资料都是用`keyCode`,`which`和`charCode`,但是文档里都建议使用`key`属性。。。所以，让我们好好看一看，到底该用哪个吧！通常来说，应该是以文档为主的。
#### key属性
上面属性的介绍，可以知道，key值返回的就是一个字符串，比如按了按键`Enter`,就返回字符串`Enter`。
> 这个就和keyCode它们有很明显的区别，它们3个都是需要靠一个对应的表格才知道这个数字对应的是哪个按键（比如keycode==13 就是回车键），而key就直接返回`enter`这样,就简单明了很多了！

举个例子：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191127164724.png)

> 如果你想知道更多key对应的值，你可以看这表格，非常的全，大部分按键都是所见即所得，[key对应值表格](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent/key/Key_Values#Whitespace_keys)

兼容性   
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191127145439.png)

举个例子：输入一个大写的M
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191127170923.png)
这里要注意一点：如果按键生成的字符即将插入某个`<input>`、`<textarea></textarea>`或其他元素，则会依次触发beforeinput,input事件。若某些实现中支持`keypress`事件则可能触发这个事件。

## 参考资料
- [KeyboardEvent(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent)
- [key对应值表格(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent/key/Key_Values#Whitespace_keys)
- [KeyboardEvent.key(MDN文档)](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent/key)


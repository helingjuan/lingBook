# HTML5 的新特性
<!-- TOC -->

- [HTML5 的新特性](#html5-的新特性)
    - [1. 新增语义化更好的标签元素](#1-新增语义化更好的标签元素)
    - [2. 增强型表单](#2-增强型表单)
    - [3. 音频和视频](#3-音频和视频)
    - [4. 新增的其他API](#4-新增的其他api)

<!-- /TOC -->

### 1. 新增语义化更好的标签元素
   - 结构元素：`aside,header,hgroup,footer,figure,section,nav`等
   - 其他元素：`video,audio,canvas,mark,progres,source`等
### 2. 增强型表单
1. 增加表单元素 `datalist, progress, meter, keygen, output`
2. 增加表单属性

| 属性 | 描述 |
| -- | -- | 
| placeholder | 输入框默认提示文字 |
| required | 是否必填 |
| pattern | 描述一个正则表达式验证输入的值 |
| min/max | 元素的最小/最大值 |
| step | 规定合法的数字间隔 |
| height/width | 宽高|
| autofocus | 是否自动获取焦点 |
| multiple | 是否支持多选 |

### 3. 音频和视频
提供和音频和视频的标准，即`<audio></audio>`和`<video></video>`,以及控制的API

### 4. 新增的其他API
  - Canvas绘图
  - svg绘图
  - 地理位置：请求用户共享他们的位置`getCurrentPosition()`。
  位置信息来源：IP地址、三维地址、GPS定位、从RFID、Wifi和蓝牙到Wifi的MAC地址、GSM或CDMA、手机的ID、用户自定义数据
  - Communication：跨文档消息通讯，可以确保iframe、标签页、窗口间安全地进行跨源通信
  - 拖放API
  - **Web Worker** 在当前js主线程中，使用Worker类加载一个js文件来开辟一个新的线程，起到互不阻塞执行的效果，并且提供主线程和新线程之间数据交换的接口：`postMessage和onMessage`
  - Websocket
  - Web Stoage：新增本地存储方案之一，意图在于**解决本来不应该是cookie做，但不得不用cookie的本地存储**：`sessionStorage` 和 `localStorge`
    - sessionStorage: 保存在session中，浏览器关闭，数据就自动清除
    - localStorage：保存在客户端本地，除非手动删除，否则会一直存在
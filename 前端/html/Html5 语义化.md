# HTML5的语义化
<!-- TOC -->

- [HTML5的语义化](#html5的语义化)
  - [为什么需要语义化](#为什么需要语义化)
  - [结构语义化](#结构语义化)
    - [头部`<header>`](#头部header)
    - [导航栏`<nav></nav>`](#导航栏navnav)
    - [`<aside></aside>`](#asideaside)
    - [`<section></section>`](#sectionsection)
    - [`<article></article>`](#articlearticle)
    - [`<figure></figure>`](#figurefigure)
    - [`<datalist></datalist>`（很少用）](#datalistdatalist很少用)
    - [`<output></output>`（很少用）](#outputoutput很少用)
    - [`<progress></progress>`](#progressprogress)
    - [`<video></video>` 和`<audio></audio>`](#videovideo-和audioaudio)
      - [`<video></video>`视频](#videovideo视频)
      - [`<audio></audio>`音频](#audioaudio音频)
      - [`<source>`](#source)
      - [用js控制视频/音频播放](#用js控制视频音频播放)
    - [`<dl></dl>,<dt></dt>`和`<dd></dd>`](#dldldtdt和dddd)
    - [`<address></address>`](#addressaddress)
    - [`<footer></footer>`](#footerfooter)
- [参考资料](#参考资料)

<!-- /TOC -->

## 为什么需要语义化

- 易维护、易修改
- 无障碍阅读支持
- 搜索引擎友好，利于SEO
- 面向未来的HTML，浏览器在未来可能提供更丰富的支持

## 结构语义化

语义元素，都仅仅是页面结构的规范化，并不会对内容有本质的影响

### 头部`<header>`

`<header></header>`都应该包含某种级别的标题，所以应隐式或显式地包含标题。
有两种用法：
- 标注内容的标题
- 标注网页的页眉

一般不在内容中使用`<header></header>`

### 导航栏`<nav></nav>`
主要用于一组文章的链接，一个页面可以包含多个`<nav></nav>`元素，但通常仅仅在页面的主要导航部分使用。
一般来说，通常使用列表`<ul></ul>`来组织链接

### `<aside></aside>`
主要用于表示与它周围文本没有密切关系的内容。
文章中同样可以使用`<aside></aside>`，用来说明文章的附加内容，解释说明某个观点，相关内容链接等。

### `<section></section>`
表示文档中的一个区块或者章节，通常会将一个标题元素`<h1>-<h6>`作为子元素
注意点：
- 不要把`<section></section>`作为一个普通的容器来使用，这种事`<div>`的使用范围。
- 通常来说`<section>`应该只被当做文档结构框架来使用

### `<article></article>`
主要用来表示自己是一个独立的内容解构，每一个`<article></article>`元素内部结构应该都是相似的。

### `<figure></figure>`
表示是一个自我独立的内容元素，通常包含一个标题说明`<figcaption></figcaption>`，内容通常会使一个图片，图标，代码片段或者和主内容相关的图解。

### `<datalist></datalist>`（很少用）
与`<select></select>`很像，里面可以防止很多`<option></option>`元素，也呈现出下拉列表的样子，但是现实的地方不一样。
这是一个数据容器，需要使用它的`<input>`元素，使用list属性，引用`<datalist></datalist>`列表，于是这个`<input>`不仅可以直接输入数据，而且可以从下拉列表中选择数据。

用法：
```
<label>从列表中选择一种浏览器：
<input list="browsers" name="myBrowser" /></label>
<datalist id="browsers">
  <option value="谷歌浏览器">
  <option value="火狐浏览器">
  <option value="IE浏览器">
  <option value="Opera浏览器">
  <option value="Safari浏览器">
</datalist>
```
### `<output></output>`（很少用）
用来输入计算结果或者用户动作的结果
### `<progress></progress>`
就是现实进度条
用法：
```
<progress value="70" max="100">70 %</progress>
```
属性：
- max 进度条的最大值，必须大于0，可以是浮点数，默认为1
- value 进度条的完成进度，必须是小于max的值


### `<video></video>` 和`<audio></audio>`
实现了HTML对视频播放和音频播放的原生支持，这样我们就可以直接将音频/视频嵌入到网页中
#### `<video></video>`视频
用法：
```
<video src="http://www.webhek.com/~j/theora_testsuite/320x240.ogg" controls autoplay loop>
  Your browser does not support the <code>video</code> element.
</video>
```

属性：
- src 资源的URL，也可以是本地的文件
- controls 显示播放和暂停按钮和进度条
- autoplay 自动播放
- loop 循环播放

#### `<audio></audio>`音频
用法：
```
<audio controls autoplay loop src="/test/audio.ogg" preload="auto">
<p>Your browser does not support the <code>audio</code> element.</p>
</audio>
```
属性：
- preload 缓存
  属性值：
    - none 不缓存
    - auto 缓存
    - metadata 只缓存文件元信息

#### `<source>`
为了兼容各种浏览器对不同媒体类型的支持，可以用多个`<source>`来提供多个不同的媒体类型。
用法：
```
// 支持Ogg格式视频流的浏览器可以播放Ogg文件，如果不支持，可以播放MPEG-4文件。
<video controls>
  <source src="foo.ogg" type="video/ogg">
  <source src="foo.mp4" type="video/mp4">
  Your browser does not support the <code>video</code> element.
</video>
```
#### 用js控制视频/音频播放
```
// 播放
var v = document.getElementsByTagName("video")[0];
v.play();
// 暂停
v.pause()
// 提高音量
v.volume += 0.1
// 减低
v.volume -= 0.1
```

### `<dl></dl>,<dt></dt>`和`<dd></dd>`
定义性列表，通常用来描述一些术语定义，比如词汇表，键值对等

### `<address></address>`
主要用来存放地址信息的，可以和`<article></article>`元素配对来提供文章作者的联想信息。
注意点：
- 如果是行文中出现的地址，不需要用`<address></address>`元素
- 建议：`<address></address>`应该放在`<footer></footer>`元素里。

> 尽管<address>元素缺省的显示样式和<i>和<em>等元素的样式相同，但当遇到涉及地址的联系信息时，使用<address>元素更合适，因为它**体现了更明确的语义信息。**

### `<footer></footer>`
用来表示整个文档或与其相应的某个区域内容的页脚。一个footer通常包含的内容有：作者信息，版权信息或相关连接。
注意点：
- `<footer></footer>`元素中的作者信息应该放在`<address></address>`元素中。
- `<footer></footer>`元素自己不能成为一个段落内容，因此，它不应在文档目录中体现出来
# 参考资料

- [IFE-NOTE：页面结构语义化——(百度IFE)](https://rainylog.com/post/ife-note-1/)
- [HTML5手册](http://know.webhek.com/html5/html-dl-dt-dd.html)
---
title: vue 播放直播视频HLS
tags: vue
notebook: 前端
---
# vue 播放直播视频HLS
其实vue是可以播放基本的mp4视频的，直接使用`video`标签即可。
但是HLS是一个比较特殊的直播视频协议，所以需要采用插件来播放。（如果不了解HLS协议的视频的话，可以看这个[直播的几种视频格式介绍（hls，rtmp等）](https://github.com/heihuahe/lingBook/blob/master/%E5%89%8D%E7%AB%AF/others/%E7%9B%B4%E6%92%AD%E7%9A%84%E5%87%A0%E7%A7%8D%E8%A7%86%E9%A2%91%E6%A0%BC%E5%BC%8F%E4%BB%8B%E7%BB%8D%EF%BC%88hls%EF%BC%8Crtmp%E7%AD%89%EF%BC%89.md)）
我试过直接用vedio标签来播放，然后失败了，就寻寻觅觅。

最后我采用`vue-video-player` 这个插件，这个插件是基于`Video.js`的。
那么就一个个介绍吧。
## 1. Video.js 简单介绍
### 1.1 为什么要用Video.js
Video.js是基于HTML5的一个网络视频播放器，它支持HTML5视频和**现代流媒体**格式，比如YouTube,Vimeo,Flash等等。
它支持在桌面PC端和**移动端**播放视频。
和HTML5视频相比，它有什么不同呢？来看看这个表格
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191122173740.png)  
:exclamation:这里划重点！！
**支持很多种流媒体，且社区环境非常好**！优秀！
### 1.2 快速使用介绍
如果你只是简单的使用，这个也许能快速的帮助到你，但是如果你的场景比较复杂，建议还是看文档！（文档地址在最后的参考资料里）
步骤：  
1. 引入`Video.js`js文件，获取方式有CDN引入，npm下载等等。注意：css和js都要引入。
2. 正常使用`<video></video>标签`加载视频，但是要添加一个额外的属性`data-setup`,这个属性必须有值，最最最少也得是个空对象`{}`,而且它可以包含Video.js的配置项，当然，必须得是JSON格式的。
   这样设置之后，当加载页面的时候，Video.js会在`video标签`中自动根据初始化并配置播放器设置；
   当然，如果你不想要这样的自动加载，你可以去掉这个属性`data-setup`，然后在js中通过`video.js`的方法初始化video标签。

#### 1.2.1 html加载即初始化
```
<video
    id="my-player"
    class="video-js"
    controls
    preload="auto"
    poster="//vjs.zencdn.net/v/oceans.png"
    data-setup='{}'>
  <source src="//vjs.zencdn.net/v/oceans.mp4" type="video/mp4"></source>
  <source src="//vjs.zencdn.net/v/oceans.webm" type="video/webm"></source>
  <source src="//vjs.zencdn.net/v/oceans.ogv" type="video/ogg"></source>
  <p class="vjs-no-js">
    To view this video please enable JavaScript, and consider upgrading to a
    web browser that
    <a href="https://videojs.com/html5-video-support/" target="_blank">
      supports HTML5 video
    </a>
  </p>
</video>
```
参数注释：  
- `poster`： 在播放前的封面图
- `data-setup`：配置项
- `<source></source>`：播放地址配置
  - src： 播放地址
  - type：文件类型
#### 1.2.2 js加载初始化
举个例子：   
```
/*js方式初始化*/
<video id="my-player"></video>
// js，方法1：默认初始化
var player = videojs('my-player');
// js，方法2：自定义初始化
var options = {}; //配置项
var player = videojs('my-player', options, function onPlayerReady() {
  videojs.log('Your player is ready!');

  // In this context, `this` is the player that was created by Video.js.
  this.play();

  // How about an event listener?
  this.on('ended', function() {
    videojs.log('Awww...over so soon?!');
  });
})
```
## 2. vue-video-player介绍
这是基于`video.js`的一个vue播放的插件，所以`video.js`所支持的视频格式或者协议，`vue-video-player`也都支持。


## 参考资料
- [vue-video-player(npm 文档)](https://www.npmjs.com/package/vue-video-player)
- [Video.js(Video.js官网)](https://videojs.com/city)
- [Video.js快速使用(github——Video.js)](https://github.com/videojs/video.js)
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
```
npm install vue-video-player --save
```
### 2.1 引用方式
#### 全局引用
在main.js中引入
```
import Vue from 'vue'
import VideoPlayer from 'vue-video-player'
// 加载video.js的样式
import 'video.js/dist/video-js.css'
// 引用
Vue.use(VideoPlayer)
```
#### 局部引用
```
import videoPlayer from 'vue-video-player'
import 'video.js/dist/video-js.css'
export defult {
  components: {
    videoPlayer
  }
}
```
### 2.2 使用介绍
这个才是最重要的地方！
这里只介绍SPA的使用方式，SSR的请去官网查看噢。
#### 2.2.1 方法1 videoPlayer
如果要使用HLS协议的视频的话，要多安装一个插件`videojs-contrib-hls`，不用的话，就不用安装
```
npm install videojs-contrib-hls --save
```
```
// ！注意：ref这个属性就相当于id，是必要的属性，因为vue是组件化思想，所以渲染时是根据ref来找到videojs实例的
<template>

  <div class="bg-303133">
      <video-player  class="video-player vjs-custom-skin" id="myVideo" ref="videoPlayer" 
        :playsinline="playsinline" :options="playerOptions" @play="onPlayerPlay($event)">
      </video-player>
  </div>
</template>

import videoPlayer from 'vue-video-player'
import hls from 'videojs-contrib-hls' // 引入hls
import '../../../node_modules/video.js/dist/video-js.css'
import '../../../node_modules/vue-video-player/src/custom-theme.css'

export default {
    components: {
        videoPlayer
    },
    data (){
      return {
        liveAddress: '', // 直播地址
        playerOptions: {} // 播放器配置文件
      }
    },
    methods: {
        onLive(onM3u8,onCover){
			      var that = this
            that.playerOptions =  {
                notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
                autoplay: true, //如果true,浏览器准备好时开始回放。
                loop: false, // 导致视频一结束就重新开始。
                // preload: 'auto', // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
                language: 'zh-CN',
                aspectRatio:"16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
                fluid: false, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
                sources: [{
                    type: "application/x-mpegURL", //如果是直播的话  此处务必这样配置，这个就是HLS视频格式的
                    src: onM3u8,//视频url地址
                }],
                poster: onCover, //你的封面地址
                width: document.documentElement.clientWidth,
                control: { //此处的设置都未生效，不知道为啥，我用爆破的方式解决的
                    timeDivider: true,
                    durationDisplay: true,
                    remainingTimeDisplay: false,
                    fullscreenToggle: true //全屏按钮
                }
                
            }
         },
         onPlayerPlay(player) {
           console.log('点了全屏')
          //全屏播放
          if (!player.isFullscreen()) {
            player.requestFullscreen();
            player.isFullscreen(true);
          } else {
            player.exitFullscreen();
            player.isFullscreen(false);
          }
        },
    },
    computed: {
      player() {
        return this.$refs.videoPlayer.player
      },
      playsinline() { //判断playsinline，在android 中为false，在ios中为true
        var ua = navigator.userAgent.toLocaleLowerCase();
        //x5内核
        if (ua.match(/tencenttraveler/) != null || ua.match(/qqbrowse/) != null) {
          return false
        }else{
          //ios端
          return true				
        }
      }
    },
    mounted() {
      this.$nextTick(() => {
        this.onLive(live_address) // 初始化视频，live_address 视频地址
      });
    }
  }
```
关于playerOptions中的source 是用来设置视频格式和视频地址的。
这里重点介绍下视频格式的配置
```
举例：
sources: [{
    type: "application/x-mpegURL", //如果是直播的话  此处务必这样配置，这个就是HLS视频格式的
    src: onM3u8,//视频url地址
}],

```
说明：
- type: "video/mp4", 这就是mp4的格式，MPEG 4文件使用 H264 视频编解码器和AAC音频编解码器
- type: 'video/webm'  WebM 文件使用 VP8 视频编解码器和 Vorbis 音频编解码器
- type: 'video/ogg' Ogg 文件使用 Theora 视频编解码器和 Vorbis音频编解码器
- type: "application/x-mpegURL"  就是流媒体格式,比如HLS

注意：前面3种格式（mp4，webm， ogg）都是video标签原生就支持的视频格式

## 参考资料
- [vue-video-player(npm 文档)](https://www.npmjs.com/package/vue-video-player)
- [Video.js(Video.js官网)](https://videojs.com/city)
- [Video.js快速使用(github——Video.js)](https://github.com/videojs/video.js)
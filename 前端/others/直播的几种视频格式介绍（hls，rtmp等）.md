---
title: 直播的几种视频格式介绍（hls，rtmp等）
tags: 视频
notebook: 前端
---
# 直播的几种视频格式介绍（hls，rtmp等）
<!-- TOC -->

- [直播的几种视频格式介绍（hls，rtmp等）](#直播的几种视频格式介绍hlsrtmp等)
  - [概述](#概述)
    - [HLS和RTMP的区别](#hls和rtmp的区别)
  - [1.HLS(HTTP Live Streaming)视频](#1hlshttp-live-streaming视频)
    - [HLS所支持的内容（算是特性吧）](#hls所支持的内容算是特性吧)
    - [HLS传输过程](#hls传输过程)
    - [HLS的优缺点](#hls的优缺点)
  - [2. RTMP(Real Time Messaging Protocol) 实时消息传送协议](#2-rtmpreal-time-messaging-protocol-实时消息传送协议)
    - [RTMP协议的优缺点](#rtmp协议的优缺点)
    - [RTMP协议的多种变种](#rtmp协议的多种变种)
  - [HTTP-FLV](#http-flv)
    - [HTTP-FLV的优缺点](#http-flv的优缺点)
  - [参考资料](#参考资料)

<!-- /TOC -->
## 概述
最近接到了一个需求，要和莹石云平台的直播地址对接，并且在移动端播放。然后给出的测试地址（hls）是这样的：`http://hls01open.ys7.com/openlive/f01018a141094b7fa138b9d0b856507b.hd.m3u8`  
目前前端支持的视频直播协议大概有这么几种：
- HLS(HTTP Live Streaming)
- RTMP(Real Time Messaging Protocol)
- HTTP-FLV

其中，RTMP是Adobe开发的协议，无法与iPhone兼容，所以目前兼容性最好的就是HLS协议的了。  
### HLS和RTMP的区别
- HLS适用于移动端使用，可用微信直接打开，也可集成H5页面嵌入到微信小程序或者微信公众号中。
- RTMP适用于PC网页端使用，可用flash或者ckplayer等播放器嵌入网页的方式播放，较HLS延迟小，更稳定。


举个例子：  
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191121112105.png)

## 1.HLS(HTTP Live Streaming)视频
HLS是苹果公司实现的基于HTTP的流媒体传输协议，可实现流媒体的直播和点播。它的工作原理是将视频流分片成一系列的基于HTTP的文件来下载，每次只下载一些，在开始一个流媒体会话时，客户端会下载一个包含元数据的extended ，所以HLS与RTMP相比，会有比较高的延迟。
M3U(m3u8) playlist 文件，用于播放可以的媒体流。
> HTTP Live Streaming (HLS) sends audio and video over HTTP from an ordinary web server for playback on iOS-based devices—including iPhone, iPad, iPod touch, and Apple TV—and on desktop computers (macOS).(**HLS其实一开始是用来发送音频或者视频给ios环境的设备，比如iPhone，iPad，macOS等。**) Using the same protocol that powers the web, HLS deploys content using ordinary web servers and content delivery networks. HLS is designed for reliability and dynamically adapts to network conditions by optimizing playback for the available speed of wired and wireless connections.
(**HLS为可靠性而设计，通过优化回放获取恰当的有线或无线的网络连接速度，从而动态适应不同的网络环境**)
————Developer

总结：HLS的工作原理：它会在服务器端将流媒体数据切割成连续的时长较短的小文件，并通过 M3U8 索引文件按序访问小文件。客户端只要不停的按序播放从服务器获取到的文件，从而实现播放音视频。
### HLS所支持的内容（算是特性吧）
- 支持播放直播和回放的视频
- 在不同比特率下有多个备用流
- 可以针对网络带宽的变化智能切换流
- 支持媒体加密和用户认证
### HLS传输过程
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191121154924.png)
大致流程：  
录制视频——> 到服务器端：视频编码成fMP4格式的文件，然后传送至**流分割器**中，——> 把文件分解成一个个mp4的小文件，然后通过HTTP传送至客户端
### HLS的优缺点
优点：  
1. Apple的全系列产品支持和Android的支持，不用安装热和插件就能原生支持播放HLS，所以说对移动端兼容的非常好；
2. 基于HTTP/80 传输，可以有效地避免被防火墙拦截；
3. 通过HTTP传输，支持网络分卡，CDN支持良好等；

缺点：  
1. 延迟较高，基本延迟在10s+以上；
2. 因为文件都被切割了，所以会有海量的小文件，对存储和缓存都有一定的挑战；
## 2. RTMP(Real Time Messaging Protocol) 实时消息传送协议
这是Adobe公司为Flash播放器和服务器之间音视频数据传输开发的私有协议。
基于TCP上的明文协议，默认使用端口1935。  
RTMP 在收发数据的时候并不是以 Message 为单位的，而是把 Message 拆分成 Chunk 发送，而且必须在一个 Chunk 发送完成之后，才能开始发送下一个 Chunk。每个 Chunk 中都带有 Message ID，表示属于哪个 Message，接收端也会按照这个 ID 将 Chunk 组装成 Message。就是说，**协议中的消息，在传输的过程中被拆分为更小的消息块(Chunk),然后将分割后的消息块通过TCP协议传输，接收端再根据接收的消息块ID把它组成消息，恢复成流媒体数据。**
### RTMP协议的优缺点
优点：  
1. 它是专为流媒体开发的协议，对底层的优化比其他协议更加优秀，同时对Adobe Flash支持好，基本上所有的编码器都支持RTMP输出；
2. 适合长时间播放；
3. 延迟相对较低，一般在1-3s之间；

缺点：  
1. 基于TCP协议，非公共端口，容易被防火墙阻拦；
2. 它是Adobe的私有协议，很多设备无法播放，特别是在ios端，需要使用第三方解码器才能播放；
### RTMP协议的多种变种
1. RTMP，默认使用TCP端口1935的纯粹协议；
2. **RTMPS**，通过一个TLS/SSL连接传输RTMP；
3. **RTMPE**，通过Adobe自有安全机制**加密的RTMP**。实现细节是私有的，但是这个加密机制用的是行业标准的密码学原函数；
4. **RTMPT**，用HTTP封装的RTMP。目的是可以穿透防火墙；
5. **RTMFP**，使用UDP协议的RTMP，这是一个安全的实时媒体流协议包，可以让最终用户直接地相互连接。

## HTTP-FLV
FLV(Flash Video)也是Adobe公司推出的一种视频格式，这是在网络上传输的流媒体数据存储容器格式。其特点是：格式相对简单轻量，不需要很大的媒体头部信息，所以加载速度就很快了。其文件后缀为`.flv`  
而HTTP-FLV 就是**将流媒体数据封装成FLV格式，然后通过HTTP协议传输给客户端**

### HTTP-FLV的优缺点
优点：  
1. 基于HTTP/80传输，可以有效地避免被防火墙拦截；
2. 可以通过HTTP 302 跳转灵活调度/负载均衡；
3. 支持使用HTTPS加密传输，也能够兼容Android，iOS的移动端；

缺点：  
1. 由于它的传输特性,会让流媒体资源缓存在本地客户端，保密性不够好；
2. 因为所需网络流量较大，也就不适合做拉流协议
## 参考资料
- [HTTP Live Streaming(苹果开发者网站)](https://developer.apple.com/documentation/http_live_streaming)
- [直播接入指南(莹石开放平台)](https://open.ys7.com/doc/zh/book/index/live_proto.html)
- [RTMP、HTTP-FLV、HLS，你了解常见的三大直播协议吗(又拍云)](https://www.upyun.com/tech/article/352/RTMP%E3%80%81HTTP-FLV%E3%80%81HLS%EF%BC%8C%E4%BD%A0%E4%BA%86%E8%A7%A3%E5%B8%B8%E8%A7%81%E7%9A%84%E4%B8%89%E5%A4%A7%E7%9B%B4%E6%92%AD%E5%8D%8F%E8%AE%AE%E5%90%97.html)
- [实时消息协议(维基百科)](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE)
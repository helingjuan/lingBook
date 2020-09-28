# HTTP相关-WebSocket了解一下

<!-- TOC -->

- [HTTP相关-WebSocket了解一下](#http相关-websocket了解一下)
  - [什么是WebSocket?](#什么是websocket)
    - [WebSocket 特点](#websocket-特点)
- [参考资料](#参考资料)

<!-- /TOC -->

## 什么是WebSocket?

WebScoket 是HTML5中的协议，支持**持久连接**，http协议不支持持久性连接，HTTP/1.1 中的keep-alive ，是将多个http请求合并为1个。

> 注意！
> HTTP中，一个请求只能对应一个响应，而且这个响应是被动的，不能主动发起。
> 这种单向请求的特点就是，如果服务器有连续的状态边哈，客户端要获知就非常麻烦，需要使用**轮询**来获取，就是每隔一段时间，就发出一个询问，了解服务器有没有新的信息。
> 最典型的场景就是聊天室
> 因为轮询的效率低，且非常浪费资源，所以就出现了WebSocket

WebSocket是基于HTTP协议的，在握手阶段与HTTP相同，但是WebSocket多了两个属性： **Upgrade**和**Connection**

### WebSocket 特点

- **服务端可以主动的向客户端推送信息**，客户端也可以主动向服务端发起信息，是真正地双向平等对话，属于**服务器推送技术**的一种
- 建立在TCP协议上
- 与HTTP协议有良好的兼容性，默认端口是80和443，并且握手阶段采用HTTP协议
- 数据格式比较轻量，性能开销小，通信高效
- 既可以发送文本，也可以发送二进制数据
- 没有同源限制，客户端可以与任意服务器通信
- 协议标识符是`ws`，加密的话是`wss`

# 参考资料
- [WebSocket 教程——(blog：阮一峰)](http://www.ruanyifeng.com/blog/2017/05/websocket.html)
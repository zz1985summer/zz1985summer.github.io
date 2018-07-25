## WebSocket  
WebSocket是一种在单个TCP连接上进行全双工通讯的协议。WebSocket通信协议于2011年被IETF定为标准RFC 6455，并由RFC7936补充规范。WebSocket API也被W3C定为标准。

WebSocket使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在WebSocket API中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。  
## Socket.io  
api: https://socket.io/docs/  
socket.io 是一个基于 engine.io 开发的封装了 websocket 功能的 nodejs 库，其实现双向通信的方式不仅仅是 websocket 还有 Flash Socket、Ajax long polling 等。目前测试 ios 9.x 微信端不支持 socket.io。
socket.io 2.0.x 在 windows 上的一个 bug 如果不指定 { wsEngine :ws } 响应速度会非常慢。而这个问题在 linux && macos 上没有。作者也说在 2.1.x 之后版本修正这个问题。  

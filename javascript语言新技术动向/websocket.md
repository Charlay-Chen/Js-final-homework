# web Socket
## 定义

WebSocket对象提供了用于创建和管理与服务器的WebSocket连接
以及用于在连接上发送和接收数据的API。
WebSocket API最伟大之处在于服务器和客户端可以在给定的时间范围内的任意时刻，相互推送信息。

## WebSocket API的用法
```javascript
// 创建一个Socket实例
var socket = new WebSocket('ws://localhost:8080'); 
// 打开Socket 
socket.onopen = function(event) { 
  // 发送一个初始化消息
  socket.send('I am the client and I\'m listening!'); 
  // 监听消息
  socket.onmessage = function(event) { 
    console.log('Client received a message',event); 
  }; 
  // 监听Socket的关闭
  socket.onclose = function(event) { 
    console.log('Client notified socket has closed',event); 
  }; 
  // 关闭Socket.... 
  socket.close() 
};
从上面这段代码中看，参数为URL，ws表示WebSocket协议。onopen、onclose和onmessage方法
把事件连接到Socket实例上。其中的onmessage事件提供了一个data属性，可以包含消息的body部分，
但必须是字符串类型。
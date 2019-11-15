> 是什么

浏览器和服务器之间建立一个不受限的双向通信的通道。利用了HTTP协议来建立连接，下层协议同样是TCP。

> 为什么http不能

这是因为HTTP协议是一个请求－响应协议，请求必须先由浏览器发给服务器，服务器才能响应这个请求，再把数据发送给浏览器。TCP协议本身就实现了全双工通信

> http轮询问题

- 实时性不够
- 频繁的请求会给服务器带来极大的压力



> 建立连接

利用http创建连接，浏览器发起

请求

```
GET ws://localhost:3000/ws/chat HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Origin: http://localhost:3000
Sec-WebSocket-Key: client-random-string
Sec-WebSocket-Version: 13
```

响应

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: server-random-string
```



> WebSocket优点

- 较少的控制开销

  在连接创建后，服务器和客户端之间交换数据时，用于协议控制的数据包头部相对较小。在不包含扩展的情况下，对于服务器到客户端的内容，此头部大小只有2至10字节（和数据包长度有关）；对于客户端到服务器的内容，此头部还需要加上额外的4字节的掩码。**相对于HTTP请求每次都要携带完整的头部，此项开销显著减少了。**

- 更强的实时性

- 保持连接状态

  Websocket需要先创建连接，这就使得其成为一种有状态的协议，之后通信时可以省略部分状态信息。**而HTTP请求可能需要在每个请求都携带状态信息（如身份认证等）。**

- 更好的二进制支持

  Websocket定义了二进制帧，**相对HTTP，可以更轻松地处理二进制内容**。




















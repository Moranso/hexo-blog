## websocket

Websocket 使用 ws 或 wss 的统一资源标志符，类似于 HTTPS，其中 wss 表示在 TLS 之上的 Websocke

默认情况下，Websocket 协议使用 80 端口；运行在 TLS 之上时，默认使用 443 端口。

#### 创建socket对象

```
// 第一个参数 url, 指定连接的 URL。第二个参数 protocol 是可选的，指定了可接受的子协议。
var Socket = new WebSocket(url, [protocol] );
```

#### 属性:

##### readyState(只读) 

0:尚未建立连接

1:连接成功

2:正在关闭练级

3:连接已关闭

#### 事件

Socket.onopen	连接建立时触发

Socket.onmessage	客户端接收服务端数据时触发

Socket.onerror	通信发生错误时触发

Socket.onclose	连接关闭时触发

#### 方法

Socket.send()	使用连接发送数据

Socket.close()	关闭连接

```
<script type="text/javascript">
 function WebSocketTest() {
 	if ("WebSocket" in window) {
 		alert("您的浏览器支持 WebSocket!");

    // 打开一个 web socket
    var ws = new WebSocket("ws://localhost:9998/echo");

	 ws.onopen = function() {
      // Web Socket 已连接上，使用 send() 方法发送数据
      ws.send("发送数据");
      alert("数据发送中...");
    };

	ws.onmessage = function (evt) { 
    var received_msg = evt.data;
    alert("数据已接收...");
  };

  ws.onclose = function() { 
    // 关闭 websocket
    alert("连接已关闭..."); 
  };
} else {
  // 浏览器不支持 WebSocket
  alert("您的浏览器不支持 WebSocket!");
	}
}
</script>
```

 
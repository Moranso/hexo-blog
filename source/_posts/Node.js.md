### 创建服务器

```
const http = require('http')
http.createServer((req, res) => {
	res.writeHead(200, {'content-type': 'text/plain'})
	res.end('Hello World')
}).listen(9999)
console.log('http://127.0.0.1:9999')
```

### 异步读文件

```
const fs = require('fs')
fs.readFile('input.text', (err, data) => {
	if (err) return console.error(err)
	console.log(data.toString())
})
```

### 同步读取文件

```
const fs = require('fs')
let data = fs.readFileSync('input.text')
```

### Node.js事件循环

- Node.js是单进程单线程应用程序,但是因为V8引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。
- Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。

### Node.js事件驱动

当web server接收到请求，就把它关闭然后进行处理，然后去服务下一个web请求。当这个请求完成，它被放回处理队列，当到达队列开头，这个结果被返回给用户。

### eventEmitter

- Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。
- events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。

```
let events = require('events')

// 创建eventEmitter对象
let eventEmitter = new events.EventEmitter()

// 创建事件处理程序
let connectHandler = () => {
  console.log('连接成功')

  // 触发data_received事件
  eventEmitter.emit('data_received')
}

eventEmitter.on('data_received', () => {
  console.log('数据接收成功')
})

// 绑定事件及事件的处理程序
eventEmitter.on('connection', connectHandler)

eventEmitter.emit('connection')
```

### Node.js Stream流

Node.js，Stream 有四种流类型：

- **Readable** - 可读操作。
- **Writable** - 可写操作。
- **Duplex** - 可读可写操作.
- **Transform** - 操作被写入数据，然后读出结果

  所有的Stream对象都是EventEmitter的实例,常用的事件有:

- ​	**data** - 当有数据可读时触发。
- ​	**end** - 没有更多的数据可读时触发。
- ​	**error** - 在接收和写入过程中发生错误时触发。
- ​	**finish** - 所有数据已被写入到底层系统时触发。

#### 从流中读取数据

```
// 引入fs模块
var fs = require('fs')

let data = ''

// 创建可读流
let readerStream = fs.createReadStream('./input.txt')
// 设置编码
readerStream.setEncoding('UTF8')
// 开始读取文件
readerStream.on('data', chunk => {
  data += chunk
})
// 读取事件失败时的事件
readerStream.on('error', err => {
  console.log('读取文件失败', err)
})
// 文件读取完毕
readerStream.on('end', () => {
  console.log('文件读取完毕,' + data)
})
```

### 写入流

```
let fs = require('fs')

let writeData = '写入的数据'

// 创建写入流,写入到output.txt文件
let writeStream = fs.createWriteStream('output.txt')

// 以utf8格式写入writeData
writeStream.write(writeData, 'UTF8')

writeStream.end()

writeStream.on('finish', () => {
  console.log('文件写入完毕')
})

writeStream.on('error', err => {
  console.log('文件写入失败,' + err)
})
```

### 管道流

管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。

```
let fs = require('fs')

let readerStream = fs.createReadStream('input.txt')

let writeStream = fs.createWriteStream('./output.txt')

// 读取input.txt文件内容,并将内容写入到output.txt文件中
readerStream.pipe(writeStream)
```

### 链式流

链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。

```
//压缩文件
fs.createReadStream('./input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'))
console.log('文件压缩完成')

//解压文件
fs.createReadStream('./input.txt.gz')
  .pipe(zlib.createGunzip())
  .pipe(fs.createWriteStream('input1.txt'))
console.log('文件解压完成')
```


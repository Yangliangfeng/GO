# GO实现千万级WebSocket消息推送服务

### 拉模式
* 原理
```
客户端定时的轮询服务端的接口，获取服务端更新的实时信息
```
* 劣势
```
1. 数据更新频率低，则大多数的请求是无效的

2. 在线用户数量多时，则服务端的查询负载很高

3. 定时轮询拉取，无法满足时效性要求
```
### 推模式
* 原理
```
一种基于客户器/服务器机制、由服务器主动将信息送到客户器的技术
```
* 优势
```
1. 仅在数据更新时才需要推送

2. 需要维护客户端与服务端的大量的在线长连接

3 数据更新后可以立即推送
```
### Websocket推送
* 选择Websocket协议的原因
```
1. 浏览器支持socket编程，轻松维持服务器端的长连接

2. 基于TCP可靠传输之上的协议，无需开发者关心通讯细节

3. 提供了高度可靠的编程接口，业务开发成本较低
```
### Websocket协议与交互

![](https://github.com/Yangliangfeng/GO/raw/master/images/9.jpg)
* 通讯流程
```
1. 客户端发送HTTP请求到服务端，这个请求的header里面带了upgrade字段，告诉服务端这个请求将升级为websocket协议。

服务端收到后将会给客户端一个握手的确认，switching字段表明服务端允许向websocket协议的转换。建立连接之后，客户端

与服务端底层的TCP协议是没有中断的。客户端可以给服务端发送基于websocket协议的消息message,服务端也可以向客户端发

送websocket协议的消息message。websocket协议发送消息的基本单位是message。
```
* 传输原理
```
1. 协议升级后，继续复用HTTP的底层socket完成后续的通讯

2. Websocket协议发送消息的基本单位是message，但是，在底层，message被切分成多个frame帧进行传输

3. 编程时只需要关心操作message,无需关心frame

4. 框架底层完成TCP网络的收发，Wbesocket协议的解析，开发者无需关系
```
* 实现HTTP服务端Go示例
```
package main
`
包名此处略去
`
function main(){
    http.HandleFunc("/ws", wsHandler)
    
    http.ListenAndServe("1270.0.1:7777", nil)
}
func wsHandler(w http.ResponseWriter, r *http.Request){
    w.Write([]byte("Hello World")
}
```
* 完成Websocket握手
```
package main

`
包名此处略去
`
var (
    upgrader = websocket.Upgrader{
        CheckOrigin: func(r *http.Request) bool {
            return true
        },
    }
)
func main(){
    http.HandlFunc("/ws", wsHandler)
    
    http.ListenAndServe("127.0.0.1:7777", nil)
}
func wsHandler(w http.ResponseWriter, r *http.Request){
    var (
        wsConn *websocket.Conn
        err error
        data []byte
    )
     //Upgrader:websocket
    if wsConn, err = upgrader.Upgrader(w, r, nil); err != nil {
        return
    }
   //websocket proctol to send and receive message
    for {
        if _, data, err = wsConn.ReadMessage(); err != nil {
            goto ERR
        }
        if err = wsConn.WriteMessage(data); err != nil {
           goto ERR
        }
    }
    ERR:
      wsConn.Close()
}
```
* 封装Websocket
```
package main

`
包名此处略去
`
var (
    upgrader = websocket.Upgrader{
        CheckOrigin: func(r *http.Request) bool {
            return true
        },
    }
)
func main(){
    http.HandlFunc("/ws", wsHandler)
    
    http.ListenAndServe("127.0.0.1:7777", nil)
}
func wsHandler(w http.ResponseWriter, r *http.Request){
    var (
        wsConn *websocket.Conn
        err error
        data []byte
        conn *WAPI.Connection
    )
     //Upgrader:websocket
    if wsConn, err = upgrader.Upgrader(w, r, nil); err != nil {
        return
    }
    if conn, err = WAPI.InitConnection(); err != nil {
        goto ERR
    }
    //test 
    go func(){
         for {
             conn.WriteMessage([]byte("heartbeat"))
             time.sleep(1 * time.Sencods)
         }
    }()
    for {
        if data, err = conn.ReadMessage(); err != nil {
            goto ERR
        }
        if err = conn.WriteMessage(data); err != nil {
            goto ERR
        }
    }
    ERR:
       wsConn.Close()
   
}
```
```
//对websocket进行封装
package WAPI

`
包名此处略去
`

type Connection struct{
    wsConn *websocket.Conn
    inChan chan []byte 
    outChan chan []byte
    closeChan chan byte
    isClose bool
    mutex sync.Mutex
}

func InitConnection(wsConn *websocket.conn) (conn *Connection, err error){
    conn = &Connection {
        wsConn: wsConn,
        inChan: make([]byte, 1000),
        outChan: make([]byte, 1000),
        closeChan: make(chan byte, 1),
    }
    
    go conn.readLoop()
    go conn.writeLoop()
    
    return
}
//API for providing
func (conn *Connection) ReadMessage() (data []byte, err error){
    select{
    case data = <- conn.inChan:
    case <- conn.closeChan:
        err = errors.New("connection already closed")
    }
    return
    
}
func (conn *Connection) WriteMessage([]byte) (err error) {
    select {
        case outChan <- data:
        case <- conn.closeChan:
            err = errors.New("connection already closed")
    }
    return
}
func (conn *Connection) Close(){
    conn.wsConn.Close()
    //只允许关闭一次
    conn.mutex.Lock()
    if !conn.isClose {
        close(conn.closeChan)
        conn.isClose = true
    }
    conn.mutex.Unlock()
    
}
//achive API func in built
func (conn *Connection) readLoop() {
    var (
        data []byte
        err error
    )
    for {
        if _, data, err = conn.wsConn.ReadMessage(); err != nil {
            goto ERR
        }
        select {
            case inChan <- data:
            case <- closeChan:
                goto ERR
        }
        
    }
    ERR:
      conn.Close()
}
func (conn *Connection) writeLoop() {
    var (
        data []byte
        err error
    )
    for {
        select{
            case data = <- outChan:
            case <- closeChan:
                 goto ERR
        }
        
        if err = conn.wsConn.WriteMessage(websocket.TextMessage, data); err != nil {
            goto ERR
        }
    }
    ERR:
      conn.Close()
}
//如果当出现err，程序会跳转到ERR关闭连接，但是，比如data =  <- outChan会阻塞住不动了，所以，加一个select选择器，当有关闭closeChan信道时，程序会跳出来。
```

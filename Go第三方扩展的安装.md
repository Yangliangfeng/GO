* gopm的安装
```
go get -u github.com/gpmgo/gopm
```

* mysql客户端的安装
```
gopm get -g -v github.com/go-sql-driver/mysql
```

* Protobuf
```
1. 概念
   轻便高效的序列化数据结构的协议，可以用于网络通信和数据存储。
   
2. github地址：
    https://github.com/protocolbuffers/protobuf

3. golang库所属地址
    https://github.com/golang/protobuf

4. window下载安装
    1）https://github.com/protocolbuffers/protobuf/releases/latest
    
    2）放在了D:\video\golang\protobuf36，然后把 D:\video\golang\protobuf36\bin  加入环境变量
       这是protobuf编译器，将.proto文件，转译成protobuf的原生数据结构
    
    3）创建文件：ProdService.proto
    
    4）goland编译器安装：Protobuf Support插件
    
    5）安装插件：
        gopm get -g -v github.com/golang/protobuf/protoc-gen-go
        此时会在你的GOPATH 的bin目录下生成可执行文件. protobuf的编译器插件protoc-gen-go
        等下我们执行protoc 命令时 就会自动调用这个插件
        
     6）安装go开发库
        go get github.com/golang/protobuf/proto
        
     7） proto语法
        https://developers.google.com/protocol-buffers/docs/proto3
      
      8）案例：
          定义个 message,代表请求部分：
          message  ProdRequest {
            int32 prod_id = 1;   //传入的商品ID
          }
          1  是为了确定参数顺序
          响应结果部分：
          message  ProdResponse {
              int32 prod_stock=1;
          }
       9）编译
          protoc --go_out=. ProdService.proto
          
          protoc --plugin=protoc-gen-go=C:\Go_project\bin\protoc-gen-go.exe --go_out=. ProdService.proto
          完整的指定路径的方式

```

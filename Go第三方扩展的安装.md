
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
          protoc --go_out=../services/ Prod.proto //指定编译生成的文件目录
          
          protoc --go_out=plugins=grpc:../services  Prod.proto
          
          protoc --plugin=protoc-gen-go=C:\Go_project\bin\protoc-gen-go.exe --go_out=. ProdService.proto
          完整的指定路径的方式

```
* Docker安装goland
```
1. docker镜像地址
   https://hub.docker.com/_/golang
   docker pull golang:1.12.7-alpine3.9
   
```
* window安装gin
```
1. 创建文件夹
   api.yang.com/topic ,切topic文件夹
   go mod init topic.jtthink.com

2. go get  github.com/gin-gonic/gin
   
3. 如果不能下载，设置如下：参考（http://www.hishenyi.com/archives/1420）
   1）window使用PowerShell设置
      $env:GO111MODULE="on"
      $env:GOPROXY="https://goproxy.io"
      goproxy.baidu.com
      或
      $env:GOPROXY="https://mirrors.aliyun.com/goproxy/"
   2）Linux
      export GO111MODULE=on 
      export GOPROXY=https://goproxy.io
```
* 验证器validator
```
1. github地址
   https://github.com/go-playground/validator
   
2. 参考文档地址
   https://godoc.org/gopkg.in/go-playground/validator.v8#hdr-Baked_In_Validators_and_Tags
   
3. 案例
    type Topic struct {
         TopicID int `json:"id" `
         TopicTitle string `json:"title" binding:"required"`
         TopicShortTitle string `json:"stitle" binding:"required,nefield=TopicTitle"`
         UserIP string `json:"ip" binding:"ip4_addr"`
         TopicScore int `json:"score" binding:"omitempty,gt=5"`
    }
```
* gorm框架的使用
```
1. 安装
   go get -u github.com/go-sql-driver/mysql //安装mysql驱动
   go get -u github.com/jinzhu/gorm

2. github地址
   https://github.com/jinzhu/gorm

3. 文档地址
   http://gorm.io/
```
* 解析ini配置文件的Go第三方库
```
go get -u  github.com/go-ini/ini

```
* go-mysql第三方库
```
1. 这不是一个纯mysql驱动。而是包含了mysql协议解析、复制（MySQL Replication）
go get -u  github.com/siddontang/go-mysql
```
* go数据库中间件
```
1. 地址
   https://github.com/xwb1989/sqlparser
```

* go-jwt
```
1. 地址
   https://github.com/dgrijalva/jwt-go

2. 下载
   go get -u github.com/dgrijalva/jwt-go
   
3. 文档地址
   https://godoc.org/github.com/dgrijalva/jwt-go#example-New--Hmac
```
* Json库
```
1. 文档
   github.com/tidwall/gjson

2. 下载
   go get -u github.com/tidwall/gjson
```
* go解析ini配置文件的另一个扩展
```
1. github地址
   https://github.com/go-ini/ini
   
2. 安装
   go get gopkg.in/ini.v1
```
* 监控配置文件并重启服务器
```
1. git地址
   https://github.com/jpillora/overseer

2. 安装
   go get -u github.com/jpillora/overseer
```
* 通过go.mod下载包
```
1. 删除出问题的go.mod和go.sum文件

2. 替换成新的go.mod文件

3. 执行 go mod download

4. 当再次安装的时候go get -u xxxxx ,不要加-u这个参数
   
```
* grpc字段的验证
```
1. github地址
   https://github.com/envoyproxy/protoc-gen-validate

2. 安装
   go get -u github.com/envoyproxy/protoc-gen-validate
```
* 解决json中tag不一致的第三方插件
```
1. github地址
   https://github.com/favadi/protoc-go-inject-tag

2. 安装
   go get -u github.com/favadi/protoc-go-inject-tag
```
* go爬虫
```
1. 第三方爬虫框架
   go get github.com/gocolly/colly
   
2. 第三方数据结构
   go get github.com/emirpasic/gods

3. headless chrome无头浏览器的组件chromedp
   https://github.com/chromedp/chromedp
   go get  github.com/chromedp/chromedp
```
* Go的交叉编译
```
set GOOS=linux
set GOARCH=amd64
go build -o build/gin main.go
```
* go的定时任务插件
```
1. 地址
   https://github.com/robfig/cron
```
* go的es扩展
```
1. 地址
   https://github.com/olivere/elastic
```

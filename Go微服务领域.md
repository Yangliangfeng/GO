### Go微服务之go-kit

* go-kit简单入门
```
1. 介绍
  https://github.com/go-kit/kit 
  
  go-kit是一个微服务工具包集合。利用它提供的API和规范可以创建健壮，可维护性高的微服务体系

2. 参考文档
  https://godoc.org/github.com/go-kit/kit
  
3. 安装
  安装: go get github.com/go-kit/kit 
  
4. 微服务体系的基本需求
  1） HTTP REST、RPC
  2） 日志功能
  3） 限流
  4） API监控
  5） 服务注册与发现
  6） API网关
  7） 服务链路追踪
  8） 服务熔断
 
5. Go-kit的三层架构
  1） Transport 
      主要负责与 HTTP、gRPC、thrift等相关的逻辑
      可以理解为是个拦截器，负责请求协议的实现和路由转发，请求和响应的序列化和反序列化
  2） Endpoint
      定义Request 和Response格式，并可以使用装饰器包装函数，以此来实现各种中间件嵌套。
      负责功能逻辑转发
  3） Service
      这里就是我们的业务类、接口等
```
* 一个第三方路由
```
1. github地址
   https://github.com/gorilla/mux

2. 安装
   go get github.com/gorilla/mux
```
* go内置限流包
```
1. 安装
  go get golang.org/x/time/rate 
  
2. 市面上比较流行的限流算法：
  1）漏桶
  2）令牌桶
  
3. Go令牌桶核心方法：
  1）Wait/WaitN    
  2）Allow/AllowN 
  3）Reserve/ReserveN 

```
### Go微服务之grpc
```
1. github地址
  https://github.com/grpc/grpc-go

2. 安装
  go get -u google.golang.org/grpc

3. grpc-gateway
  https://github.com/grpc-ecosystem/grpc-gateway

```
### Go微服务之go-micro
```
1. github地址
  https://github.com/micro/go-micro

2. 安装
  go get -u github.com/micro/go-micro

3. 命令行注册多个服务
  1）添加  Init()
  2) 命令行 go run prod_main.go --server_address :8080
  
4. go-micro第三方插件库
  1）github地址
    https://github.com/micro/go-plugins
  
  2）安装
    go get github.com/micro/go-plugins

5. go-micro支持protoc第三方插件
  1）安装
    go get github.com/micro/protoc-gen-micro
    
6. 装饰器
  https://github.com/micro/go-plugins/tree/master/wrapper
```

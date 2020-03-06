### RabbitMQ入门

* 介绍
```
RabbitMQ是基于Erlang语言开发的，基于AMQP(Advanced Message Queue Protocol 高级消息队列协议)协议实现的消息队列

它是一种应用程序之间的通信方法。
```
* 应用场景
```
1. 任务的异步处理

将不需要同步处理的并且耗时很长的操作由消息队列通知消息接收方进行异步处理。

2. 应用程序的解耦合

MQ相当于一个中介，生产方通过MQ与消费方交互，它将应用程序进行解耦合
```
* RabbitMQ的工作原理

![](https://github.com/Yangliangfeng/GO/raw/master/images/rmqp.png)
```
组成部分说明：
  
  1. Broker:消息队列服务进程，此进程包括两个部分：Exchange和Queue
  
  2. Exchange:消息队列交换机，按照一定规则将消息路由转发到某个队列，对消息进行过滤
  
  3. Queue：消息队列，存储消息的队列，消息到达队列并转发给指定的消费方
  
  4. Producer：消息的生产者，即生产客户端，生产客户端将消息发送到MQ
  
  5. Consumer：消息消费者，即消费客户端，接收MQ转发的消息
  
  
消息的发送接收流程
  -----发送消息-----
  
  1. 生产者和Broker建立TCP连接
  
  2. 生产者和Broker建立会话通道
  
  3. 生产者通过通道将消息发送给Broker，由交换机将消息进行转发
  
  4. Exchange将消息转发到指定的Queue（队列）
  
  -------接收消息-------
  
  1. 消费者和Broker建立TCP连接
  
  2. 消费者和Broker建立会话通道
  
  3. 消费者监听指定的Queue（队列）
  
  4. 当有消息到达Queue时，Broker默认将消息推送给消费者
  
  5. 消费者接收消息

```
* RabbitMQ工作模式
```
1. Work Queue 工作队列模式

2. Publish/Subscribe 发布订阅

3. Routing 路由模式

4. Topics 通配符模式

5. Header Header转发器

6. RPC 远程过程调用
```

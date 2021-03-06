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
* Exchange 交换机
```
交换机的类型：

1. fanout: 对应的rabbitmq的工作模式：Publish/Subscribe 发布订阅

2. direct: 对应的routing工作模式

3. topic: 对应的Topics工作模式

4. headers: 对应的Headers工作模式

```

* Publish/Subscribe 发布订阅

![](https://github.com/Yangliangfeng/GO/raw/master/images/r_ps.png)
```
发布订阅模式：

1.一个生产者将消息发给交换机

2. 与交换机绑定的有多个队列，每个消费者监听自己的队列
```
* Work Queue 工作队列模式

![](https://github.com/Yangliangfeng/GO/raw/master/images/r_wq.png)
```
工作队列模式:

1. 一个生产者将消息发送给一个队列

2. 多个消费者共同监听一个队列

3. 消息不能重复消费

4. rabbitmq采用轮询的方式将消费平均发给消费者
```
* MQ重要参数的说明(go语言版本的rabbitmq为准)
```
1. publish发送消息
   mandatory：此参数设置为true，在exchange正常且可到达的情况下，如果exchange+routeKey无法投递给queue
   
   那么MQ会将消息返还给生产者；如果为false时，则直接丢弃
```
* 延迟交换机插件
```
1. 下载地址
  https://github.com/rabbitmq/rabbitmq-delayed-message-exchange

2. 拷贝到容器中
   docker cp rabbitmq_delayed_message_exchange-3.8.0.ez rmq:/opt/rabbitmq/plugins
   
3. 启用插件
  rabbitmq-plugins enable rabbitmq_delayed_message_exchange

4. 查看启用的插件
  rabbitmq-plugins list
```

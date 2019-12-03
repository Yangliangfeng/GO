## 优化篇

* apache的ab压力测试返回值说明
```
ab -n 100 -c 50 ------总共100个请求，50个并发

Document Length:        xxxx bytes       HTTP响应数据的正文长度

Time taken for tests:  xxxxx seconds    所有请求处理完成所花费的时间

Complete requests:      xxxx             完成请求数

Failed requests:        0                失败请求数

Total transferred:      xxxxxx bytes     网络总传输量

HTML transferred:       xxxx bytes     HTML内容传输

Requests per second:    xxxx  [#/sec] (mean) 吞吐量-每秒请求

Time per request:       xxx[ms] (mean)  每一次(用户)请求响应时间  (Time taken for tests/次数)
在这里就是"次数" = 100/50

Time per request:       xxx  [ms] (mean, across all concurrent requests) 并发的每个请求平均消耗时间
  (上面一个Time per request/并发数)

Transfer rate:  网络传输速度
```
* 句柄数的设置
 ```
 1. 查看句柄数
    ulimit -a   查看所有的参数
    ulimit -n   查看句柄数
    
 2. 查看指定进程ID的句柄数
    lsof -p ID  | wc -l
 
 3. 设置
    sudo vi /etc/security/limits.conf 
    用户名   soft nofile 100000
    用户名   hard nofile 100000
    * hard nofile 100000 //*表示所有的用户
 ```
 * ab的压测命令 ：ab -c 1500 -n 3000 -k http://139.196.x.x:8080/v1/prods?size=10 //-k 是持久连接
 
 * go的压测工具
 `
  https://github.com/rakyll/hey
 `

### Elasticsearch

* docker安装elasticsearch环境
```
1. docker地址：
   https://hub.docker.com/r/blacktop/elasticsearch

2. 拉取镜像
   docker pull blacktop/elasticsearch:7.4

3. 镜像的tag
   docker tag blacktop/elasticsearch:7.4 es:74

4. github地址
   https://github.com/blacktop/docker-elastic-stack

5. 启动
   docker run -d --name es  -p 9200:9200 es:74

6. 拉取kabana镜像
   docker pull blacktop/kibana:7.4

```

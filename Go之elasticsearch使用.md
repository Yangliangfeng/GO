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
* go的elasticsearch的客户端搭建
```
1. 地址
   https://github.com/olivere/elastic/

2. 安装
   go get github.com/olivere/elastic/v7
   
3. 启动kabana
   docker run -d --init --name kb -e elasticsearch.hosts="139.196.228.149:9200" \
   -p 5601:5601 kb:74
```
* 中文分词器
```
1. 下载地址
   https://github.com/medcl/elasticsearch-analysis-ik/releases
   
2. 拷贝运行的es容器内elasticsearch文件夹到本地
   docker cp es:/usr/share/elasticsearch /home/shenyi/es74

3. 新建ik文件夹
   /home/yang/es74/elasticsearch/plugins
   并把下载的ik分词的压缩包解压后拷贝至/home/yang/es74/elasticsearch/plugins/ik文件夹下
   
4. 运行容器
   docker run -d --name es\
    -v /home/yang/es74/elasticsearch:/usr/share/elasticsearch  \
   -p 9200:9200 es:74

5.ik分析器
   ES内部的分析器由：分词器和过滤器组成
   
   ik有两个 ik_smart 和ik_max_word， ik_max_word颗粒度更细
   
   POST _analyze
   {
     "analyzer": "standard",
      "text" : "程序教程"
   }
```

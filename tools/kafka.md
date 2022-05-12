## docker部署kafka（[参考](https://www.jianshu.com/p/0edcc3addf3f)）


### 1、拉取镜像

#### 拉取kafka、zookeeper镜像
  docker pull wurstmeister/zookeeper

  docker pull wurstmeister/kafka

### 拉取kafka-mananger

  docker pull sheepkiller/kafka-manager

### 2、kafka、zookeeper定义docker-compose.yml
```
version: '3'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    restart: always
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    restart: always
    depends_on: [ zookeeper ]
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 192.168.160.30
      KAFKA_CREATE_TOPICS: "test:1:1"
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /data/product/zj_bigdata/data/kafka/docker.sock:/var/run/docker.sock
```


### 3、打包|启动
1>:打包

docker-compose build

2>:启动

docker-compose up -d

3>:管理工具：

docker run -itd --name=kafka-manager -p 9000:9000 -e ZK_HOSTS="192.168.160.30:2181" sheepkiller/kafka-manager
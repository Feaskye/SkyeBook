参照：https://www.jianshu.com/p/0edcc3addf3f


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
    +
      KAFKA_ADVERTISED_HOST_NAME: 192.168.1.104
      KAFKA_CREATE_TOPICS: "test:1:1"
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /data/product/zj_bigdata/data/kafka/docker.sock:/var/run/docker.sock


开机启动：image标签下同级加入
    restart: always
管理工具：
docker run -itd --name=kafka-manager -p 9000:9000 -e ZK_HOSTS="192.168.1.104:2181" sheepkiller/kafka-manager
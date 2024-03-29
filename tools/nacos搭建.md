# [使用Docker部署Nacos-Server(单机版)](https://www.jianshu.com/p/3d3e17bc629f )

## 初始准备
    docker pull nacos/nacos-server

    mkdir -p /home/nacos/logs/                      #新建logs目录
    mkdir -p /home/nacos/init.d/          
    vim /home/nacos/init.d/custom.properties        #修改配置文件

## 配置
    server.contextPath=/nacos
    server.servlet.contextPath=/nacos
    server.port=8848

    spring.datasource.platform=mysql

    db.num=1
    db.url.0=jdbc:mysql://xx.xx.xx.x:3306/nacos_devtest_prod?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
    db.user=user
    db.password=pass


    nacos.cmdb.dumpTaskInterval=3600
    nacos.cmdb.eventTaskInterval=10
    nacos.cmdb.labelTaskInterval=300
    nacos.cmdb.loadDataAtStart=false

    management.metrics.export.elastic.enabled=false

    management.metrics.export.influx.enabled=false


    server.tomcat.accesslog.enabled=true
    server.tomcat.accesslog.pattern=%h %l %u %t "%r" %s %b %D %{User-Agent}i


    nacos.security.ignore.urls=/,/**/*.css,/**/*.js,/**/*.html,/**/*.map,/**/*.svg,/**/*.png,/**/*.ico,/console-fe/public/**,/v1/auth/login,/v1/console/health/**,/v1/cs/**,/v1/ns/**,/v1/cmdb/**,/actuator/**,/v1/console/server/**
    nacos.naming.distro.taskDispatchThreadCount=1
    nacos.naming.distro.taskDispatchPeriod=200
    nacos.naming.distro.batchSyncKeyCount=1000
    nacos.naming.distro.initDataRatio=0.9
    nacos.naming.distro.syncRetryDelay=5000
    nacos.naming.data.warmup=true
    nacos.naming.expireInstance=true


## 启动容器
- 2.0.3或2.1版本
docker  run \
--name nacos -d \
-p 8848:8848 \
-p 9848:9848 \
-p 9849:9849 \
--privileged=true \
--restart=always \
--net=host \
-e JVM_XMS=256m \
-e JVM_XMX=256m \
-e MODE=standalone \
-e PREFER_HOST_MODE=hostname \
-v /home/nacos/logs:/home/nacos/logs \
-v /home/nacos/data:/home/nacos/data \
-v /home/nacos/conf:/home/nacos/conf \
-v /home/nacos/init.d/custom.properties:/home/nacos/init.d/custom.properties \
nacos/nacos-server




- 配置有参版本
docker  run \
--name nacos -d \
-p 8848:8848 \
-p 9848:9848 \
-p 9849:9849 \
--privileged=true \
--restart=always \
-e JVM_XMS=256m \
-e JVM_XMX=256m \
-e MODE=standalone \
-e PREFER_HOST_MODE=hostname \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=172.17.0.4 \
-e MYSQL_SERVICE_PORT=3307 \
-e MYSQL_SERVICE_DB_NAME=egg_config \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=123456 \
-e MYSQL_DATABASE_NUM=1 \
-v /home/nacos/logs:/home/nacos/logs \
-v /home/nacos/data:/home/nacos/data \
-v /home/nacos/conf:/home/nacos/conf \
nacos/nacos-server




-v /home/nacos/conf:/home/nacos/conf \
tail -n 100 /home/nacos/logs/start.out


- 1.3版本：
docker  run \
--name nacos -d \
-p 8848:8848 \
--privileged=true \
--restart=always \
-e JVM_XMS=256m \
-e JVM_XMX=256m \
-e MODE=standalone \
-e PREFER_HOST_MODE=feaskye \
-v /home/nacos/logs:/home/nacos/logs \
-v /home/nacos/data:/home/nacos/data \
-v /home/nacos/conf:/home/nacos/conf \
-v /home/nacos/init.d/custom.properties:/home/nacos/init.d/custom.properties \
nacos/nacos-server:1.3.0

tail -n 100 /home/nacos/logs/start.out


### windows：1.3成功
<!-- docker  run --name nacos -d -p 8848:8848 -p 9848:9848 -p 9849:9849 --privileged=true --restart=always -e JVM_XMS=256m -e JVM_XMX=256m -e MODE=standalone -v D:\ProgramFiles\Docker\Containers\nacos\logs:/home/nacos/logs -v D:\ProgramFiles\Docker\Containers\nacos\data:/home/nacos/data -v D:\ProgramFiles\Docker\Containers\nacos\init.d\custom.properties:/home/nacos/init.d/custom.properties nacos/nacos-server -->


<!-- docker  run --name nacos2.0.0 -d -p 8848:8848 -p 9848:9848 -p 9849:9849 --privileged=true --restart=always -e JVM_XMS=256m -e JVM_XMX=256m -e MODE=standalone -v D:\ProgramFiles\Docker\Containers\nacos\logs:/home/nacos/logs -v D:\ProgramFiles\Docker\Containers\nacos\data:/home/nacos/data -v D:\ProgramFiles\Docker\Containers\nacos\init.d\custom.properties:/home/nacos/init.d/custom.properties nacos/nacos-server:2.0.0 -->

docker  run --name nacos1.3.0 -d -p 8848:8848 -p 9848:9848 -p 9849:9849 --privileged=true --restart=always -e JVM_XMS=256m -e JVM_XMX=256m -e MODE=standalone -v D:\ProgramFiles\Docker\Containers\nacos\logs:/home/nacos/logs -v D:\ProgramFiles\Docker\Containers\nacos\data:/home/nacos/data -v D:\ProgramFiles\Docker\Containers\nacos\init.d\custom.properties:/home/nacos/init.d/custom.properties nacos/nacos-server:1.3.0



## 访问
    http://localhost:8848/nacos/#/configurationManagement?dataId=&group=&appName=&namespace=&pageSize=&pageNo=






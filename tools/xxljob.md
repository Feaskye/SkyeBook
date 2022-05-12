## 一、XXl_job docker部署

### 1：首先创建本地配置文件（[源码](https://github.com/xuxueli/xxl-job)）（[参考](https://www.jianshu.com/p/0ca5f622bff8)）
找到git源文件复制进系统，并做数据库连接更改，以xxl-job-admin:2.2.0为例

    /home/xxl-job/application.properties

### 2：创建日志文件
    /home/xxl-job/applogs

### 3：创建docker容器
--net host  使用宿主ip和端口（使用此配置可以不用配置步骤3中的mysql权限）  
-e PARAMS 指定了外部的配置文件

    docker run -p 8070:8080 -d --name xxl-job-admin -v /home/xxl-job/application.properties:/application.properties --net host -v /home/xxl-job/applogs:/data/applogs -e PARAMS='--spring.config.location=/application.properties' xuxueli/xxl-job-admin:2.2.0



### 然后启动并访问xxl项目：
http://localhost:8080/xxl-job-admin/toLogin





## 二、常见问题
1：无法访问mysql问题，查看网络是否为同一个网络或重启linux
2：links mysql容器

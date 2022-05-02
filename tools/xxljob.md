## 一、XXl_job docker部署

### 1：首先创建本地配置文件（[源码](https://github.com/xuxueli/xxl-job)）
找到git源文件复制进系统，并做数据库连接更改

    /home/xxl-job/application.properties

### 2：创建日志文件
    /home/xxl-job/applogs

### 3：创建docker容器
    docker run -p 8070:8080 -d --name xxl-job-admin -v /home/xxl-job/application.properties:/application.properties --net host -v /home/xxl-job/applogs:/data/applogs -e PARAMS='--spring.config.location=/application.properties' xuxueli/xxl-job-admin:2.2.0


### 然后启动并访问xxl项目：
http://localhost:8080/xxl-job-admin/toLogin





## 二、常见问题
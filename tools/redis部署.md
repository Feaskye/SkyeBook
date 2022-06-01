## docker安装redis（[参考](https://www.csdn.net/tags/MtTaEgzsMjYxNDExLWJsb2cO0O0O.html)）

- 1：拉取

`docker pull redis`

- 2：修改redis.conf配置文件： 主要配置的如下：

下载redis.conf文件

wget http://download.redis.io/redis-stable/redis.conf


```
bind 127.0.0.1 # 这行要注释掉，解除本地连接限制

protected-mode no # 默认yes，如果设置为yes，则只允许在本机的回环连接，其他机器无法连接。

daemonize no # 默认no 为不守护进程模式，docker部署不需要改为yes，docker run -d本身就是后台启动，不然会冲突

requirepass 123456 # 设置密码

appendonly yes # 持久化
```



- 3:创建本地与docker映射的目录，即本地存放的位置
  
`mkdir /data/redis`
`mkdir /data/redis/data`

- 4：要是按照挂载目录方式就直接把这个扔到挂载目录去重启redis，要是在docker内部就cp过去重启redis

sudo docker cp /home/redis/redis.conf/redis.conf  容器ID:/etc/redis/redis.conf

- 5：启动
  
    `
    docker run -p 6380:6379 --name redis -v /data/redis/redis.conf:/etc/redis/redis.conf  -v /data/redis/data:/data --restart=always -d redis redis-server 
    /etc/redis/redis.conf --appendonly yes
    `
    
    `
    docker run -p 6379:6379 --name redis -v D:/ProgramFiles/Docker/Containers/redis/redis.conf:/etc/redis/redis.conf  -v D:/ProgramFiles/Docker/Containers/redis/data:/data --restart=always -d redis redis-server
    `
参数解释：

    -p 6379:6379:把容器内的6379端口映射到宿主机6379端口 
    -v /data/redis/redis.conf:/etc/redis/redis.conf：把宿主机配置好的redis.conf放到容器内的这个位置中 
    -v /data/redis/data:/data：把redis持久化的数据在宿主机内显示，做数据备份 
    redis-server /etc/redis/redis.conf：这个是关键配置，让redis不是无配置启动，而是按照这个redis.conf的配置启动 
    –appendonly yes：redis启动后数据持久化





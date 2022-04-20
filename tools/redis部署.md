## docker安装redis

- 1：拉取

`docker pull redis`

- 2：修改redis.conf配置文件： 主要配置的如下：
`
bind 127.0.0.1 #注释掉这部分，使redis可以外部访问 daemonize no#用守护线程的方式启动 
requirepass 你的密码#给redis设置密码 
appendonly yes#redis持久化　　默认是no tcp-keepalive 300 #防止出现远程主机强迫关闭了一个现有的连接的错误 默认是300
`

- 3:创建本地与docker映射的目录，即本地存放的位置
  
`mkdir /data/redis`
`mkdir /data/redis/data`

- 4：启动
  
    `
    docker run -p 6380:6379 --name redis -v /data/redis/redis.conf:/etc/redis/redis.conf  -v /data/redis/data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes
    `
    
参数解释：

    -p 6379:6379:把容器内的6379端口映射到宿主机6379端口 -v /data/redis/redis.conf:/etc/redis/redis.conf：把宿主机配置好的redis.conf放到容器内的这个位置中 -v /data/redis/data:/data：把redis持久化的数据在宿主机内显示，做数据备份 redis-server /etc/redis/redis.conf：这个是关键配置，让redis不是无配置启动，而是按照这个redis.conf的配置启动 –appendonly yes：redis启动后数据持久化


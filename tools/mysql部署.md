## 1：切换进入root
    sudo -i

普通Linux系统：遵循systemctl命令
windows下Linux：
    （无效）开机启动docker：/lib/systemd/systemd-sysv-install enable docker
    （无效） ubuntu： sudo ln -s /lib/systemd/system/docker.service /etc/systemd/system/display-mananger.service
    另尝试systemd配置开机自启动：https://www.jianshu.com/p/dddd2bd3b59d
    开启服务： service docker start/stop/status/restart

如使用sysv-rc-conf开机启动（chkconfig已失效时），则文件中加入源包：
    vi /etc/apt/sources.list
    尾部加入：deb http://archive.ubuntu.com/ubuntu/ trusty main universe restricted multiverse
    sudo apt-get update
    sudo apt-get install sysv-rc-conf
    
    sysv-rc-conf docker on

#脚本启动测试如下：
https://blog.csdn.net/u013554213/article/details/86584705

mysql：https://www.cnblogs.com/stm32stm32/p/7862503.html
https://blog.csdn.net/weixin_27038245/article/details/113205595
https://blog.csdn.net/tcliuwenwen/article/details/108799404


开启镜像：docker start mysqldb
进入镜像：docker attach mysqldb
sudo docker run --name=mysqldb -it -p 3306:3306 -v /opt/data/mysql/mysqld:/var/run/mysqld -v /opt/data/mysql/db:/var/lib/mysql -v /opt/data/mysql/conf:/etc/mysql/conf.d -v /opt/data/mysql/files:/var/lib/mysql-files -e MYSQL_ROOT_PASSWORD=123456 --privileged=true -d mysql
sudo docker run --name=mysql57 -it -p 3307:3306 -v /opt/data/mysql57/db:/var/lib/mysql -v /opt/data/mysql57/conf:/etc/mysql/conf.d -v /opt/data/mysql57/files:/var/lib/mysql-files -e MYSQL_ROOT_PASSWORD=123456 --privileged=true -d mysql:5.7

开机启动容器： docker update --restart=always mysql57

#==============
mssql:https://www.cnblogs.com/taylorshi/p/11143497.html

docker run --name=mssql2017 -it -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=sa123456' -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
/var/opt/mssql/data/MSDBLog.ldf



-- 查看端口
netstat -apn|grep 3306
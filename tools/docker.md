Docker是一个用于开发，发布和运行应用程序的开放平台。

Docker使您能够将应用程序与基础架构分开，从而可以快速交付软件。

借助Docker，您可以以与管理应用程序相同的方式来管理基础架构。

通过利用Docker的方法来快速交付，测试和部署代码，您可以大大减少编写代码和在生产环境中运行代码之间的延迟。

其安装命令如下：

    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    sudo yum-config-manager --enable docker-ce-edge
    sudo yum-config-manager --enable docker-ce-test
    sudo yum-config-manager --disable docker-ce-edge
    sudo yum install -y docker-ce







docker rm -f 容器id
docker rmi imageId
docker logs  -tf --tail 200 nacos
docker inspect mysql57
docker network ls
docker exec -it nacos /bin/bash


mklink /j "C:\Program Files\Docker" "D:\ProgramFiles\Docker"
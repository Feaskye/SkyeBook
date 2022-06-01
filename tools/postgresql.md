### docker安裝

#### linux中docker安装：
`
docker run --name postgres \
    --restart=always \
    -e POSTGRES_PASSWORD=123456 \
    -p 5432:5432 \
    -v /data/postgresql:/var/lib/postgresql/data \
    -d postgres
`


#### win中docker安装：
`
docker run --name postgres --restart=always -e POSTGRES_PASSWORD=123456 -p 5432:5432 -v D:\ProgramFiles\Docker\Containers/postgresql:/var/lib/postgresql/data -d postgres
`
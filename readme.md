#无法上传下载

    git config --local --unset http.proxy
    git config --local --unset https.proxy
    -- 也可能是代理问题
    git config --local http.proxy 127.0.0.1:7890
    git config --local https.proxy 127.0.0.1:7890

    git config --local http.sslVerify "false"

    git config --local --unset credential.helper

    --最后一个生效
    git config --local http.sslBackend "openssl"


    查看：https://blog.csdn.net/qq_37555071/article/details/114260533

#上传大文件

    1：下载https://git-lfs.github.com/
    2：添加大文件后缀到 .gitattributes
    3:如下命令
    git config lfs.https://github.com/Feaskye/feaskye.github.io.git/info/lfs.access basic
    git config lfs.https://github.com/Feaskye/feaskye.github.io.git/info/lfs.locksverify false


#SwitchyOmega 配置地址
https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
temp:https://suo.y-t-/-CKU0CnU




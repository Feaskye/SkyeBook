#无法上传下载

    git config --global --unset http.proxy
    git config --global --unset https.proxy
    -- 也可能是代理问题
    git config --global http.proxy 127.0.0.1:7890
    git config --global https.proxy 127.0.0.1:7890

    git config --global http.sslVerify "false"

    git config --global --unset credential.helper

    --最后一个生效
    git config --global http.sslBackend "openssl"


    查看：https://blog.csdn.net/qq_37555071/article/details/114260533

#上传大文件

    1：下载https://git-lfs.github.com/
    2：添加大文件后缀到 .gitattributes
    3:如下命令
    git config lfs.https://github.com/Feaskye/feaskye.github.io.git/info/lfs.access basic
    git config lfs.https://github.com/Feaskye/feaskye.github.io.git/info/lfs.locksverify false




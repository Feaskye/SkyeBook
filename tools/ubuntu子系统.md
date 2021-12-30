# 开机启动某些服务

window10下执行:

C:\Users\用户名\AppData\Local\Microsoft\WindowsApps\ubuntu1804.exe config --default-user root

子系统下执行:

编辑 /etc/profile

vim /etc/profile

再尾部增加

service docker start
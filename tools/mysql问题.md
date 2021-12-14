 ### 无法登录问题
    到linux中执行mysql命令
    update user set host='%' where user='root';

    》mysql5.7
    update user set authentication_string=password('123456') where user='root';
    》mysql5.7后
    alter user 'root'@'%' identified with mysql_native_password by '123456';

    flush privileges;
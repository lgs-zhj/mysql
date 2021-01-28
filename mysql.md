#1.真机通过改配置文件跳过密码库修改（不知道原密码的情下况，需要root权限）
]# systemctl  stop  mysqld
]# vim /etc/my.cnf
[mysqld]
skip-grant-tables
#validate_password_policy=0
#validate_password_length=6
:wq
]# systemctl  start  mysqld
]# mysql  连接服务
mysql> select  host , user ,  authentication_string from mysql.user;
mysql> update mysql.user set  authentication_string=password("A...qqq321") 
    -> where
    -> host="localhost" and  user="root" ;
mysql> flush privileges;
mysql> exit
]# vim /etc/my.cnf
[mysqld]
#skip-grant-tables
validate_password_policy=0
validate_password_length=6
:wq
]# systemctl  restart mysqld
[root@host50 ~]# mysql -uroot -pA...qqq321
mysql> 


#2.通过mysqladmin修改密码（重置密码）,需要输入原密码.
[root@host50 ~]# mysqladmin -hlocalhost  -uroot  -p  password "123456"
Enter password:输入旧密码
[root@host50 ~]# mysql -uroot -p123456
mysql> 


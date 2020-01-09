```
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
```

```
 yum -y install mysql57-community-release-el7-10.noarch.rpm
```


```
yum --enablerepo=mysql57-community  install mysql-community-server
systemctl   start  mysqld
```

查看密码

```
grep 'temporary password' /var/log/mysqld.log 
2019-07-11T15:43:07.497595Z 1 [Note] A temporary password is generated for root@localhost: 8uyoyru=hLYR
```

修改密码

```
mysqladmin -u root -p8uyoyru=hLYR password 123456
```

密码过于简单 执行失败


取消密码复杂度检查


/etc/my.cnf
```
[mysqld]
plugin-load=validate_password.so
validate-password=OFF
```

```
systemctl  restart mysqld
```


再次修改为弱口令

```
mysqladmin -u root -p8uyoyru=hLYR password 123456
```

仅仅有警告但是修改为弱口令成功 

测试登陆


```
mysql -uroot -p123456
```













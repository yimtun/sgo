```
CREATE DATABASE test;


use test;

CREATE TABLE IF NOT EXISTS `host`(
   `id` INT UNSIGNED AUTO_INCREMENT,
   `host` VARCHAR(100) NOT NULL,
   `ip` VARCHAR(40) NOT NULL,
   PRIMARY KEY ( `id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



```
mysql> desc host;
+-------+------------------+------+-----+---------+----------------+
| Field | Type             | Null | Key | Default | Extra          |
+-------+------------------+------+-----+---------+----------------+
| id    | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| host  | varchar(100)     | NO   |     | NULL    |                |
| ip    | varchar(40)      | NO   |     | NULL    |                |
+-------+------------------+------+-----+---------+----------------+
3 rows in set (0.02 sec)
```

```
mysql   -uroot -p123456 -e "grant all privileges on test.* to webuser@'%.%.%.%' identified by '123456';"
```


测试


```
mysql -uwebuser -h172.16.99.2 -p123456
```




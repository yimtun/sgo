```
curl -d "hostname=aliyuan&hostip=172.16.99.10"     http://127.0.0.1/page
```


```
mysql -uroot -p123456 -e "select * from test.host;"
mysql: [Warning] Using a password on the command line interface can be insecure.
+----+----------+---------------+
| id | host     | ip            |
+----+----------+---------------+
|  1 | idc-vm-1 | 172.16.99.122 |
|  2 | ali-vm-1 | 192.168.1.10  |
|  3 | aliyuan  | 172.16.99.10  |
|  4 | aliyuan  | 172.16.99.10  |
+----+----------+---------------+
```

The hostname of your db server node

```
hostname -f

ip-172-31-4-66.us-west-2.compute.internal

```


The command and output for display your database server's version

```
mysql -V
mysql  Ver 15.1 Distrib 5.5.54-MariaDB, for Linux (x86_64) using readline 5.1
```

The command and output for listing your created databases

```
mysql -uroot -pcloudera


Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 12
Server version: 5.5.54-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
9 rows in set (0.00 sec)
```
```
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.9/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1
```


Installation failed the first time, because there was already a SCM database
```
sudo /usr/share/cmf/schema/scm_prepare_database.sh -uroot -pcloudera -h172.31.4.66 mysql scm scm
Enter SCM password:
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
[                          main] DbProvisioner                  ERROR Exception when creating/dropping database with user 'root' and jdbc url 'jdbc:mysql://172.31.4.66/?useUnicode=true&characterEncoding=UTF-8'
java.sql.SQLException: Can't create database 'scm'; database exists
        at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:964)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3973)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3909)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2527)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2680)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2497)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2455)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.StatementImpl.executeInternal(StatementImpl.java:839)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.StatementImpl.execute(StatementImpl.java:739)[mysql-connector-java.jar:5.1.41]
        at com.cloudera.enterprise.dbutil.DbProvisioner.executeSql(DbProvisioner.java:286)[db-common-5.9.1.jar:]
        at com.cloudera.enterprise.dbutil.DbProvisioner.doMain(DbProvisioner.java:95)[db-common-5.9.1.jar:]
        at com.cloudera.enterprise.dbutil.DbProvisioner.main(DbProvisioner.java:110)[db-common-5.9.1.jar:]
[                          main] DbProvisioner                  ERROR Stack Trace:
java.sql.SQLException: Can't create database 'scm'; database exists
        at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:964)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3973)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3909)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2527)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2680)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2497)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2455)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.StatementImpl.executeInternal(StatementImpl.java:839)[mysql-connector-java.jar:5.1.41]
        at com.mysql.jdbc.StatementImpl.execute(StatementImpl.java:739)[mysql-connector-java.jar:5.1.41]
        at com.cloudera.enterprise.dbutil.DbProvisioner.executeSql(DbProvisioner.java:286)[db-common-5.9.1.jar:]
        at com.cloudera.enterprise.dbutil.DbProvisioner.doMain(DbProvisioner.java:95)[db-common-5.9.1.jar:]
        at com.cloudera.enterprise.dbutil.DbProvisioner.main(DbProvisioner.java:110)[db-common-5.9.1.jar:]
--> Error 1, giving up (use --force if you wish to ignore the error)
```

I had to remove that database to be avle to continue.

```
mysql -uroot -pcloudera -h172.31.4.66
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 16
Server version: 5.5.54-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> drop database scm;
Query OK, 0 rows affected (0.00 sec)
```

Then I could restart my script:
```
sudo /usr/share/cmf/schema/scm_prepare_database.sh -ujakub -pcloudera -h172.31.4.66 --scm-host ip-172-31-11-167.us-west-2.compute.internal mysql scm scm
Enter SCM password:
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```

*I forgot to add with grant option - lost 20 minutes on that .... :)  "
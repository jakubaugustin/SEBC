## Verify user privileges

```
INFO  : Compiling command(queryId=hive_20170309091111_b257b8af-9b41-45f5-b106-82c34834769b): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deseri                                                                                                    alizer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20170309091111_b257b8af-9b41-45f5-b106-82c34834769b); Time tak                                                                                                    en: 0.682 seconds
INFO  : Executing command(queryId=hive_20170309091111_b257b8af-9b41-45f5-b106-82c34834769b): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20170309091111_b257b8af-9b41-45f5-b106-82c34834769b); Time tak                                                                                                    en: 0.246 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (2.146 seconds)
```



## Ferdinand and George roles

```
klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: george@TESTCLUSTER.COM

Valid starting       Expires              Service principal
03/09/2017 09:33:10  03/10/2017 09:33:10  krbtgt/TESTCLUSTER.COM@TESTCLUSTER.COM
        renew until 03/16/2017 09:33:10
[root@node0 ~]# beeline
Beeline version 1.1.0-cdh5.8.4 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM
scan complete in 3ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM
Enter username for jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM: george
Enter password for jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM: ********
Connected to: Apache Hive (version 1.1.0-cdh5.8.4)
Driver: Hive JDBC (version 1.1.0-cdh5.8.4)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20170309093636_a08887fc-e344-44de-8c7e-8e200b5203d5): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20170309093636_a08887fc-e344-44de-8c7e-8e200b5203d5); Time taken: 0.059 seconds
INFO  : Executing command(queryId=hive_20170309093636_a08887fc-e344-44de-8c7e-8e200b5203d5): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20170309093636_a08887fc-e344-44de-8c7e-8e200b5203d5); Time taken: 0.134 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.307 seconds)
0: jdbc:hive2://localhost:10000/default> Closing: 0: jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM
[root@node0 ~]# kinit ferdinand
Password for ferdinand@TESTCLUSTER.COM:
[root@node0 ~]# beeline
Beeline version 1.1.0-cdh5.8.4 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM
scan complete in 3ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM
Enter username for jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM: ferdinand
Enter password for jdbc:hive2://localhost:10000/default;principal=hive/node0.testcluster@TESTCLUSTER.COM:
Connected to: Apache Hive (version 1.1.0-cdh5.8.4)
Driver: Hive JDBC (version 1.1.0-cdh5.8.4)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20170309093737_360bffd8-05bd-47ec-8ba2-f7c958b2cacd): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20170309093737_360bffd8-05bd-47ec-8ba2-f7c958b2cacd); Time taken: 0.065 seconds
INFO  : Executing command(queryId=hive_20170309093737_360bffd8-05bd-47ec-8ba2-f7c958b2cacd): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20170309093737_360bffd8-05bd-47ec-8ba2-f7c958b2cacd); Time taken: 0.136 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.316 seconds)
0: jdbc:hive2://localhost:10000/default>

```
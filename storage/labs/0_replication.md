# HDFS Lab: Replicate to another cluster

## Name a source directory after your GitHub handle
```
sudo -u jakubaugustin hadoop fs -mkdir -p /tmp/jakubaugustin
```

## Name a target directory after your partner's GitHub handle
```
sudo -u jakubaugustin hadoop fs -mkdir -p /tmp/giorgio-sonra
```

## Use teragen to create a 500 MB file
```
$ time sudo -u jakubaugustin yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen\
 -Dmapred.map.tasks=1\
 5000000\
 /tmp/jakubaugustin/teragen
```

## Copy your partner's file to your target directory

We used CM Backup utility to perform distcp.

By default this did not work. The following changes to our setup needed to be done:
 - dfs.datanode.use.datanode.hostname changed to true (checked in CM GUI)
 - Data nodes and Namenodes had to be binded to wildcards - to run on every network interface
 - Partner cluster hosts had to be manually added to /etc/hosts on every node of target custer
 
 After that the cluster was configured for HDFS multi-homing.
 
 Replication resuts in CM:
 
<center><img src="0_replication.png"/></center>

## Browse the results

Check source files:
```
$ hdfs fsck /tmp/jakubaugustin -files -blocks

Connecting to namenode via http://node1.testcluster:50070
FSCK started by jakub (auth:SIMPLE) from /172.31.1.215 for path /tmp/jakubaugustin at Tue Mar 07 12:11:52 UTC 2017
/tmp/jakubaugustin <dir>
/tmp/jakubaugustin/teragen <dir>
/tmp/jakubaugustin/teragen/_SUCCESS 0 bytes, 0 block(s):  OK

/tmp/jakubaugustin/teragen/part-m-00000 500000000 bytes, 4 block(s):  OK
0. BP-125970560-172.31.15.231-1488829938286:blk_1073743694_2870 len=134217728 Live_repl=3
1. BP-125970560-172.31.15.231-1488829938286:blk_1073743695_2871 len=134217728 Live_repl=3
2. BP-125970560-172.31.15.231-1488829938286:blk_1073743696_2872 len=134217728 Live_repl=3
3. BP-125970560-172.31.15.231-1488829938286:blk_1073743697_2873 len=97346816 Live_repl=3

Status: HEALTHY
 Total size:    500000000 B
 Total dirs:    2
 Total files:   2
 Total symlinks:                0
 Total blocks (validated):      4 (avg. block size 125000000 B)
 Minimally replicated blocks:   4 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Tue Mar 07 12:11:52 UTC 2017 in 3 milliseconds


The filesystem under path '/tmp/jakubaugustin' is HEALTHY
```

Check target files:
```
$ hdfs fsck /tmp/giorgio-sonra/ -files -blocks

Connecting to namenode via http://node1.testcluster:50070
FSCK started by jakub (auth:SIMPLE) from /172.31.1.215 for path /tmp/giorgio-sonra/ at Tue Mar 07 12:19:49 UTC 2017
/tmp/giorgio-sonra/ <dir>
/tmp/giorgio-sonra/teragen <dir>
/tmp/giorgio-sonra/teragen/_SUCCESS 0 bytes, 0 block(s):  OK

/tmp/giorgio-sonra/teragen/part-m-00000 500000000 bytes, 4 block(s):  OK
0. BP-125970560-172.31.15.231-1488829938286:blk_1073744256_3432 len=134217728 Live_repl=3
1. BP-125970560-172.31.15.231-1488829938286:blk_1073744258_3434 len=134217728 Live_repl=3
2. BP-125970560-172.31.15.231-1488829938286:blk_1073744259_3435 len=134217728 Live_repl=3
3. BP-125970560-172.31.15.231-1488829938286:blk_1073744260_3436 len=97346816 Live_repl=3

Status: HEALTHY
 Total size:    500000000 B
 Total dirs:    2
 Total files:   2
 Total symlinks:                0 (Files currently being written: 1)
 Total blocks (validated):      4 (avg. block size 125000000 B)
 Minimally replicated blocks:   4 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Tue Mar 07 12:19:49 UTC 2017 in 2 milliseconds


The filesystem under path '/tmp/giorgio-sonra/' is HEALTHY
```
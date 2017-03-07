#HDFS Lab: Test HDFS performance

##Create an end-user Linux account named with your GitHub handle
Add user entry for all hosts:
```
$ for i in {0..4};\
  do ssh -t node$i sudo useradd jakubaugustin; \
done
 ```

Create HDFS home directory for this user:
```
$ sudo -u hdfs hadoop fs -mkdir -p /user/jakubaugustin
$ sudo -u hdfs hadoop fs -touchz /user/jakubaugustin/hello-jakubaugustin
$ sudo -u hdfs hadoop fs -chown -R jakubaugustin:jakubaugustin /user/jakubaugustin
$ sudo -u jakubaugustin hadoop fs -ls

-rw-r--r--   3 jakubaugustin jakubaugustin          0 2017-03-06 21:26 hello-jakubaugustin
``` 

##Create a 10 GB file using teragen

```
$ time sudo -u jakubaugustin yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen\
 -Dmapred.map.tasks=4\
 -Ddfs.block.size=33554432\
 100000000\
 /user/jakubaugustin/teragen
 ```
 
 Check what was generated:
 ```
 sudo -u jakubaugustin hadoop fs -ls teragen
 
-rw-r--r--   3 jakubaugustin jakubaugustin          0 2017-03-06 22:05 teragen/_SUCCESS
-rw-r--r--   3 jakubaugustin jakubaugustin 2500000000 2017-03-06 22:05 teragen/part-m-00000
-rw-r--r--   3 jakubaugustin jakubaugustin 2500000000 2017-03-06 22:05 teragen/part-m-00001
-rw-r--r--   3 jakubaugustin jakubaugustin 2500000000 2017-03-06 22:05 teragen/part-m-00002
-rw-r--r--   3 jakubaugustin jakubaugustin 2500000000 2017-03-06 22:05 teragen/part-m-00003

 ```
 
 Check generated file size:
 ```
 sudo -u jakubaugustin hadoop fs -du -h | grep teragen
 
 9.3 G    27.9 G  teragen
 ```
 
 Check that blocksize is 32 MB
 ```
 sudo -u jakubaugustin hadoop fs -stat %o /user/jakubaugustin/teragen/part-m-00000
 
 33554432
 ```
 
 ## Use Terasort for 10GB file
 
 ```
$ time sudo -u jakubaugustin yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar terasort\
 /user/jakubaugustin/teragen /user/jakubaugustin/terasort
 
         File System Counters
                FILE: Number of bytes read=4446212097
                FILE: Number of bytes written=8826875684
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=10000040200
                HDFS: Number of bytes written=10000000000
                HDFS: Number of read operations=918
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=12
        Job Counters
                Launched map tasks=300
                Launched reduce tasks=6
                Data-local map tasks=300
                Total time spent by all maps in occupied slots (ms)=2399541
                Total time spent by all reduces in occupied slots (ms)=720525
                Total time spent by all map tasks (ms)=2399541
                Total time spent by all reduce tasks (ms)=720525
                Total vcore-seconds taken by all map tasks=2399541
                Total vcore-seconds taken by all reduce tasks=720525
                Total megabyte-seconds taken by all map tasks=2457129984
                Total megabyte-seconds taken by all reduce tasks=737817600
        Map-Reduce Framework
                Map input records=100000000
                Map output records=100000000
                Map output bytes=10200000000
                Map output materialized bytes=4342784689
                Input split bytes=40200
                Combine input records=0
                Combine output records=0
                Reduce input groups=100000000
                Reduce shuffle bytes=4342784689
                Reduce input records=100000000
                Reduce output records=100000000
                Spilled Records=200000000
                Shuffled Maps =1800
                Failed Shuffles=0
                Merged Map outputs=1800
                GC time elapsed (ms)=32515
                CPU time spent (ms)=1434350
                Physical memory (bytes) snapshot=146453598208
                Virtual memory (bytes) snapshot=484263411712
                Total committed heap usage (bytes)=171929763840
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10000000000
        File Output Format Counters
                Bytes Written=10000000000
17/03/06 22:21:28 INFO terasort.TeraSort: done

real    7m48.402s
user    0m9.564s
sys     0m0.427s

 ```
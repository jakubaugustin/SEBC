The full teragen command and job output

```
time sudo -u neymar yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen\
>  -Ddfs.block.size=16777216\
>  65536000\
>  /user/neymar/tgen640
17/03/10 09:27:17 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-11-167.us-west-2.compute.internal/172.31.11.167:8032
17/03/10 09:27:17 INFO terasort.TeraSort: Generating 65536000 using 2
17/03/10 09:27:17 INFO mapreduce.JobSubmitter: number of splits:2
17/03/10 09:27:17 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
17/03/10 09:27:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1489137535019_0001
17/03/10 09:27:18 INFO impl.YarnClientImpl: Submitted application application_1489137535019_0001
17/03/10 09:27:18 INFO mapreduce.Job: The url to track the job: http://ip-172-31-11-167.us-west-2.compute.internal:8088/proxy/application_1489137535019_0001/
17/03/10 09:27:18 INFO mapreduce.Job: Running job: job_1489137535019_0001
17/03/10 09:27:24 INFO mapreduce.Job: Job job_1489137535019_0001 running in uber mode : false
17/03/10 09:27:24 INFO mapreduce.Job:  map 0% reduce 0%
17/03/10 09:27:37 INFO mapreduce.Job:  map 10% reduce 0%
17/03/10 09:27:40 INFO mapreduce.Job:  map 17% reduce 0%
17/03/10 09:27:43 INFO mapreduce.Job:  map 21% reduce 0%
17/03/10 09:27:47 INFO mapreduce.Job:  map 24% reduce 0%
17/03/10 09:27:50 INFO mapreduce.Job:  map 27% reduce 0%
17/03/10 09:27:53 INFO mapreduce.Job:  map 30% reduce 0%
17/03/10 09:27:56 INFO mapreduce.Job:  map 32% reduce 0%
17/03/10 09:27:59 INFO mapreduce.Job:  map 35% reduce 0%
17/03/10 09:28:02 INFO mapreduce.Job:  map 38% reduce 0%
17/03/10 09:28:05 INFO mapreduce.Job:  map 41% reduce 0%
17/03/10 09:28:08 INFO mapreduce.Job:  map 44% reduce 0%
17/03/10 09:28:11 INFO mapreduce.Job:  map 47% reduce 0%
17/03/10 09:28:14 INFO mapreduce.Job:  map 49% reduce 0%
17/03/10 09:28:17 INFO mapreduce.Job:  map 52% reduce 0%
17/03/10 09:28:20 INFO mapreduce.Job:  map 55% reduce 0%
17/03/10 09:28:23 INFO mapreduce.Job:  map 57% reduce 0%
17/03/10 09:28:26 INFO mapreduce.Job:  map 61% reduce 0%
17/03/10 09:28:29 INFO mapreduce.Job:  map 64% reduce 0%
17/03/10 09:28:32 INFO mapreduce.Job:  map 67% reduce 0%
17/03/10 09:28:35 INFO mapreduce.Job:  map 69% reduce 0%
17/03/10 09:28:38 INFO mapreduce.Job:  map 72% reduce 0%
17/03/10 09:28:41 INFO mapreduce.Job:  map 75% reduce 0%
17/03/10 09:28:44 INFO mapreduce.Job:  map 78% reduce 0%
17/03/10 09:28:47 INFO mapreduce.Job:  map 81% reduce 0%
17/03/10 09:28:50 INFO mapreduce.Job:  map 84% reduce 0%
17/03/10 09:28:53 INFO mapreduce.Job:  map 85% reduce 0%
17/03/10 09:28:54 INFO mapreduce.Job:  map 86% reduce 0%
17/03/10 09:28:56 INFO mapreduce.Job:  map 88% reduce 0%
17/03/10 09:28:57 INFO mapreduce.Job:  map 89% reduce 0%
17/03/10 09:29:00 INFO mapreduce.Job:  map 92% reduce 0%
17/03/10 09:29:03 INFO mapreduce.Job:  map 95% reduce 0%
17/03/10 09:29:06 INFO mapreduce.Job:  map 98% reduce 0%
17/03/10 09:29:08 INFO mapreduce.Job:  map 100% reduce 0%
17/03/10 09:29:09 INFO mapreduce.Job: Job job_1489137535019_0001 completed successfully
17/03/10 09:29:09 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=245844
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=170
                HDFS: Number of bytes written=6553600000
                HDFS: Number of read operations=8
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=4
        Job Counters
                Launched map tasks=2
                Other local map tasks=2
                Total time spent by all maps in occupied slots (ms)=201866
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=201866
                Total vcore-seconds taken by all map tasks=201866
                Total megabyte-seconds taken by all map tasks=206710784
        Map-Reduce Framework
                Map input records=65536000
                Map output records=65536000
                Input split bytes=170
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=1098
                CPU time spent (ms)=99380
                Physical memory (bytes) snapshot=385830912
                Virtual memory (bytes) snapshot=3170975744
                Total committed heap usage (bytes)=403177472
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=140750829423462787
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=6553600000
```


The result of the time command

```
real    1m54.647s
user    0m5.960s
sys     0m0.258s

```


The command and output of hdfs dfs -ls /user/neymar/tgen640

```
hdfs dfs -ls /user/neymar/tgen640

Found 3 items
-rw-r--r--   3 neymar neymar          0 2017-03-10 09:29 /user/neymar/tgen640/_SUCCESS
-rw-r--r--   3 neymar neymar 3276800000 2017-03-10 09:29 /user/neymar/tgen640/part-m-00000
-rw-r--r--   3 neymar neymar 3276800000 2017-03-10 09:29 /user/neymar/tgen640/part-m-00001
```


The command and output to show how many blocks are stored under this directory

```
hdfs fsck /user/neymar/tgen640 -files -blocks

...
Status: HEALTHY
 Total size:    6553600000 B
 Total dirs:    1
 Total files:   3
 Total symlinks:                0
 Total blocks (validated):      392 (avg. block size 16718367 B)
 Minimally replicated blocks:   392 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          4
 Number of racks:               1
FSCK ended at Fri Mar 10 09:31:12 UTC 2017 in 24 milliseconds

```
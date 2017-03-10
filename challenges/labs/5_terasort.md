```
kinit neymar


Password for neymar@JAKUBAUGUSTIN.ES:

[centos@ip-172-31-11-167 ~]$  time  yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar terasort\
>  -Dmapred.map.tasks=4\
>  /user/neymar/tgen640\
>  /user/neymar/tsort640m
17/03/10 10:08:43 INFO terasort.TeraSort: starting

17/03/10 10:08:44 INFO hdfs.DFSClient: Created token for neymar: HDFS_DELEGATION_TOKEN owner=neymar@JAKUBAUGUSTIN.ES, renewer=yarn, realUser=, issueDate=1489140524884, maxDate=1489745324884, sequenceNumber=1, masterKeyId=2 on 172.31.11.167:8020
17/03/10 10:08:44 INFO security.TokenCache: Got dt for hdfs://ip-172-31-11-167.us-west-2.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.11.167:8020, Ident: (token for neymar: HDFS_DELEGATION_TOKEN owner=neymar@JAKUBAUGUSTIN.ES, renewer=yarn, realUser=, issueDate=1489140524884, maxDate=1489745324884, sequenceNumber=1, masterKeyId=2)
17/03/10 10:08:45 INFO input.FileInputFormat: Total input paths to process : 2
Spent 476ms computing base-splits.
Spent 11ms computing TeraScheduler splits.
Computing input splits took 487ms
Sampling 10 splits of 392
Making 8 from 100000 sampled records
Computing parititions took 1453ms
Spent 1943ms computing partitions.
17/03/10 10:08:46 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-11-167.us-west-2.compute.internal/172.31.11.167:8032
17/03/10 10:08:47 INFO mapreduce.JobSubmitter: number of splits:392
17/03/10 10:08:47 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
17/03/10 10:08:47 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1489140327516_0001
17/03/10 10:08:47 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.11.167:8020, Ident: (token for neymar: HDFS_DELEGATION_TOKEN owner=neymar@JAKUBAUGUSTIN.ES, renewer=yarn, realUser=, issueDate=1489140524884, maxDate=1489745324884, sequenceNumber=1, masterKeyId=2)
17/03/10 10:08:48 INFO impl.YarnClientImpl: Submitted application application_1489140327516_0001
17/03/10 10:08:48 INFO mapreduce.Job: The url to track the job: http://ip-172-31-11-167.us-west-2.compute.internal:8088/proxy/application_1489140327516_0001/
17/03/10 10:08:48 INFO mapreduce.Job: Running job: job_1489140327516_0001
17/03/10 10:08:57 INFO mapreduce.Job: Job job_1489140327516_0001 running in uber mode : false
17/03/10 10:08:57 INFO mapreduce.Job:  map 0% reduce 0%
17/03/10 10:09:07 INFO mapreduce.Job:  map 1% reduce 0%
17/03/10 10:09:14 INFO mapreduce.Job:  map 2% reduce 0%

...


17/03/10 10:15:08 INFO mapreduce.Job: Job job_1489140327516_0001 completed successfully
17/03/10 10:15:08 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=2905391360
                FILE: Number of bytes written=5798564616
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=6553659976
                HDFS: Number of bytes written=6553600000
                HDFS: Number of read operations=1200
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=16
        Job Counters
                Launched map tasks=392
                Launched reduce tasks=8
                Data-local map tasks=392
                Total time spent by all maps in occupied slots (ms)=3271977
                Total time spent by all reduces in occupied slots (ms)=730436
                Total time spent by all map tasks (ms)=3271977
                Total time spent by all reduce tasks (ms)=730436
                Total vcore-seconds taken by all map tasks=3271977
                Total vcore-seconds taken by all reduce tasks=730436
                Total megabyte-seconds taken by all map tasks=3350504448
                Total megabyte-seconds taken by all reduce tasks=747966464
        Map-Reduce Framework
                Map input records=65536000
                Map output records=65536000
                Map output bytes=6684672000
                Map output materialized bytes=2843088150
                Input split bytes=59976
                Combine input records=0
                Combine output records=0
                Reduce input groups=65536000
                Reduce shuffle bytes=2843088150
                Reduce input records=65536000
                Reduce output records=65536000
                Spilled Records=131072000
                Shuffled Maps =3136
                Failed Shuffles=0
                Merged Map outputs=3136
                GC time elapsed (ms)=40671
                CPU time spent (ms)=1467740
                Physical memory (bytes) snapshot=191241457664
                Virtual memory (bytes) snapshot=633161101312
                Total committed heap usage (bytes)=224306659328
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=6553600000
        File Output Format Counters
                Bytes Written=6553600000
17/03/10 10:15:08 INFO terasort.TeraSort: done

real    6m25.870s
user    0m10.209s
sys     0m0.392s
```
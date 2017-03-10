kinit ronaldo
Password for ronaldo@JAKUBAUGUSTIN.ES:
[ronaldo@ip-172-31-4-66 centos]$ time  yarn jar /opt/cloudera/parcels/CDH/lib/ha                                                                                                                                   doop-mapreduce/hadoop-mapreduce-examples.jar pi 10 100\
>
Number of Maps  = 10
Samples per Map = 100
Wrote input for Map #0
Wrote input for Map #1
Wrote input for Map #2
Wrote input for Map #3
Wrote input for Map #4
Wrote input for Map #5
Wrote input for Map #6
Wrote input for Map #7
Wrote input for Map #8
Wrote input for Map #9
Starting Job
17/03/10 10:10:08 INFO client.RMProxy: Connecting to ResourceManager at ip-172-3                                                                                                                                   1-11-167.us-west-2.compute.internal/172.31.11.167:8032
17/03/10 10:10:09 INFO hdfs.DFSClient: Created token for ronaldo: HDFS_DELEGATIO                                                                                                                                   N_TOKEN owner=ronaldo@JAKUBAUGUSTIN.ES, renewer=yarn, realUser=, issueDate=14891                                                                                                                                   40609232, maxDate=1489745409232, sequenceNumber=2, masterKeyId=2 on 172.31.11.16                                                                                                                                   7:8020
17/03/10 10:10:09 INFO security.TokenCache: Got dt for hdfs://ip-172-31-11-167.u                                                                                                                                   s-west-2.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.11.                                                                                                                                   167:8020, Ident: (token for ronaldo: HDFS_DELEGATION_TOKEN owner=ronaldo@JAKUBAU                                                                                                                                   GUSTIN.ES, renewer=yarn, realUser=, issueDate=1489140609232, maxDate=14897454092                                                                                                                                   32, sequenceNumber=2, masterKeyId=2)
17/03/10 10:10:09 INFO input.FileInputFormat: Total input paths to process : 10
17/03/10 10:10:10 INFO mapreduce.JobSubmitter: number of splits:10
17/03/10 10:10:10 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_14                                                                                                                                   89140327516_0002
17/03/10 10:10:10 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Serv                                                                                                                                   ice: 172.31.11.167:8020, Ident: (token for ronaldo: HDFS_DELEGATION_TOKEN owner=                                                                                                                                   ronaldo@JAKUBAUGUSTIN.ES, renewer=yarn, realUser=, issueDate=1489140609232, maxD                                                                                                                                   ate=1489745409232, sequenceNumber=2, masterKeyId=2)
17/03/10 10:10:10 INFO impl.YarnClientImpl: Submitted application application_14                                                                                                                                   89140327516_0002
17/03/10 10:10:10 INFO mapreduce.Job: The url to track the job: http://ip-172-31                                                                                                                                   -11-167.us-west-2.compute.internal:8088/proxy/application_1489140327516_0002/
17/03/10 10:10:10 INFO mapreduce.Job: Running job: job_1489140327516_0002
17/03/10 10:10:26 INFO mapreduce.Job: Job job_1489140327516_0002 running in uber mode : false
17/03/10 10:10:26 INFO mapreduce.Job:  map 0% reduce 0%
17/03/10 10:10:35 INFO mapreduce.Job:  map 10% reduce 0%
17/03/10 10:10:42 INFO mapreduce.Job:  map 40% reduce 0%
17/03/10 10:10:46 INFO mapreduce.Job:  map 50% reduce 0%
17/03/10 10:10:47 INFO mapreduce.Job:  map 70% reduce 0%
17/03/10 10:10:48 INFO mapreduce.Job:  map 80% reduce 0%
17/03/10 10:10:49 INFO mapreduce.Job:  map 100% reduce 0%
17/03/10 10:10:56 INFO mapreduce.Job:  map 100% reduce 100%
17/03/10 10:10:56 INFO mapreduce.Job: Job job_1489140327516_0002 completed successfully
17/03/10 10:10:56 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=98
                FILE: Number of bytes written=1368739
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=3000
                HDFS: Number of bytes written=215
                HDFS: Number of read operations=43
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
        Job Counters
                Launched map tasks=10
                Launched reduce tasks=1
                Data-local map tasks=10
                Total time spent by all maps in occupied slots (ms)=96711
                Total time spent by all reduces in occupied slots (ms)=5304
                Total time spent by all map tasks (ms)=96711
                Total time spent by all reduce tasks (ms)=5304
                Total vcore-seconds taken by all map tasks=96711
                Total vcore-seconds taken by all reduce tasks=5304
                Total megabyte-seconds taken by all map tasks=99032064
                Total megabyte-seconds taken by all reduce tasks=5431296
        Map-Reduce Framework
                Map input records=10
                Map output records=20
                Map output bytes=180
                Map output materialized bytes=340
                Input split bytes=1820
                Combine input records=0
                Combine output records=0
                Reduce input groups=2
                Reduce shuffle bytes=340
                Reduce input records=20
                Reduce output records=0
                Spilled Records=40
                Shuffled Maps =10
                Failed Shuffles=0
                Merged Map outputs=10
                GC time elapsed (ms)=579
                CPU time spent (ms)=7590
                Physical memory (bytes) snapshot=4652990464
                Virtual memory (bytes) snapshot=17505763328
                Total committed heap usage (bytes)=5336203264
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=1180
        File Output Format Counters
                Bytes Written=97
Job Finished in 47.961 seconds
Estimated value of Pi is 3.14800000000000000000

real    0m57.450s
user    0m7.977s
sys     0m0.406s

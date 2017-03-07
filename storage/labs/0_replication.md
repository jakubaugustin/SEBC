# HDFS Lab: Replicate to another cluster

## Name a source directory after your GitHub handle
```
sudo -u jakubaugustin hadoop fs -mkdir -p /tmp/jakubaugustin
```

## Name a target directory after your partner's GitHub handle
```
```

## Use teragen to create a 500 MB file
```
$ time sudo -u jakubaugustin yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen\
 -Dmapred.map.tasks=1\
 5000000\
 /tmp/jakubaugustin/teragen
```
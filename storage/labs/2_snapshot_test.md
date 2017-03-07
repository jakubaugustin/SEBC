# HDFS Lab: Test HDFS Snapshots

## Create the precious directory in HDFS; copy the ZIP course file into it.

Create directory
```
$ sudo -u jakubaugustin hadoop fs -mkdir -p /user/jakubaugustin/precious
```

Copy REPO zip into it:
```
sudo su jakubaugustin
$ cd ~
$ wget https://github.com/jakubaugustin/SEBC/archive/master.zip
$ chmod 775 ./master.zip
$ hadoop fs -put ./master.zip precious/
$ rm -f master.zip
```

Check that my file is in HDFS:
```
$ sudo -u jakubaugustin hadoop fs -ls precious/master.zip

-rw-r--r--   3 jakubaugustin jakubaugustin     601641 2017-03-07 10:14 precious/master.zip
```

Check my file`s checksum before deleting it:
```
$ sudo -u jakubaugustin hadoop fs -checksum precious/master.zip

precious/master.zip     MD5-of-0MD5-of-512CRC32C        000002000000000000000000b8359dee8f3a222226ccbcab5d41897c
```

## Enable snapshots for precious
```
$ sudo -u hdfs hdfs dfsadmin -allowSnapshot /user/jakubaugustin/precious

Allowing snaphot on /user/jakubaugustin/precious succeeded
```

## Create a snapshot called sebc-hdfs-test
```
$ sudo -u jakubaugustin hadoop fs -createSnapshot /user/jakubaugustin/precious sebc-hdfs-test

Created snapshot /user/jakubaugustin/precious/.snapshot/sebc-hdfs-test
```

Check that snapshot was created
```
$ sudo -u jakubaugustin hadoop fs -ls precious/.snapshot

drwxr-xr-x   - jakubaugustin jakubaugustin          0 2017-03-07 09:58 precious/.snapshot/sebc-hdfs-test
```

## Delete the directory
```
$ sudo -u jakubaugustin hadoop fs -rm -r -f precious

rm: Failed to move to trash: hdfs://node1.testcluster:8020/user/jakubaugustin/precious: The directory /user/jakubaugustin/precious cannot be deleted since /user/jakubaugustin/precious is snapshottable and already has snapshots
```
*Directory can`t be removed since it is snapshottable and already has a snapshot in it*

## Delete the ZIP file
```
$ sudo -u jakubaugustin hadoop fs -rm -skipTrash precious/master.zip

Deleted precious/master.zip
```

## Restore the deleted file

Check my existing snaphottable directories:
```
$ sudo -u jakubaugustin hdfs lsSnapshottableDir

drwxr-xr-x 0 jakubaugustin jakubaugustin 0 2017-03-07 10:19 1 65536 /user/jakubaugustin/precious
```

List files in my snapshot:
```
$ sudo -u jakubaugustin hadoop fs -ls precious/.snapshot/sebc-hdfs-test

Found 1 items
-rw-r--r--   3 jakubaugustin jakubaugustin     601641 2017-03-06 22:39 precious/.snapshot/sebc-hdfs-test/master.zip
```

Restore my file:
```
sudo -u jakubaugustin hadoop fs -cp precious/.snapshot/sebc-hdfs-test/master.zip precious
```

And check that it is not corrupted:
```
$ sudo -u jakubaugustin hadoop fs -ls precious/master.zip

-rw-r--r--   3 jakubaugustin jakubaugustin     601641 2017-03-07 10:21 precious/master.zip

$ sudo -u jakubaugustin hadoop fs -checksum precious/master.zip

precious/master.zip     MD5-of-0MD5-of-512CRC32C        000002000000000000000000b8359dee8f3a222226ccbcab5d41897c
```

*File timestamp has changed but checksum remains the same after recovering from snapshot*








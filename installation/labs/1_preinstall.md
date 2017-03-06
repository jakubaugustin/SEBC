# System Configuration Checks

## Check vm.swappiness on all your nodes

Check swapiness level
```
$ cat /proc/sys/vm/swappiness
```

Setting VM swappiness to 1 - using kernel newer than 2.6
```
$ echo "vm.swappiness = 1" >> /etc/sysctl.conf 
$ echo 1 > /proc/sys/vm/swappiness
```

## Show the mount attributes of all volumes
I decided to use 100 GB SSD volume for OS and 200 GB Throughput optimized HDD for data.
I use the following mount schema:
 - Whole SSD is mounted under /
 - Whole HDD is mounted under /data/hdd_0
```
cat /etc/fstab

...
UUID=ef6ba050-6cdc-416a-9380-c14304d0d206 /                       xfs     defaults        0 0
UUID=48bb98ef-e950-43ab-9ede-f29532f92e68 /data/hdd_0           ext4    defaults,nofail 0 2
```

## Show the reserve space of any non-root, ext-based volumes

I use xfs for whole SSD volume.
For ext4 HDD:

```
# To find out devices
$ lsblk

NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  100G  0 disk
+-xvda1 202:1    0  100G  0 part /
xvdb    202:16   0  200G  0 disk /data/hdd_0
```

/dev/xvdb is the ext4 partition that needt to be evaluated

```
# To find out reserverd block count:
$ sudo tune2fs -l /dev/xvdb | grep "Reserved block count:"
Reserved block count:     2621440

#And to find out how big one block actually is:
$ sudo tune2fs -l /dev/xvdb | grep "Block size:"
Block size:               4096
```

So 2621440 * 4096 bytes is reserved. In total that is: 10GB which is 5% of the volume.


## Disable transparent hugepage support

To verify if THP is enabled.
```
$ cat /sys/kernel/mm/transparent_hugepage/defrag
[always] madvise never
$ cat /sys/kernel/mm/transparent_hugepage/enabled
[always] madvise never
```

Add the following to the bottom of /etc/rc.d/rc.local
```
if test -f /sys/kernel/mm/transparent_hugepage/enabled; then
echo never > /sys/kernel/mm/transparent_hugepage/enabled
fi
if test -f /sys/kernel/mm/transparent_hugepage/defrag; then
echo never > /sys/kernel/mm/transparent_hugepage/defrag
fi
```

Make rc.local file executable
```
$ chmod u+x /etc/rc.d/rc.local
```
Reboot
```
$ init 6
```

To verfiy if THP is disabled.
```
$ cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]
$ cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
```

To run it on all the other hosts:
```
for i in {1..4};\
 do echo "now doing node$i";\
 ssh -t node$i sudo cp /etc/rc.d/rc.local ~;\
 scp node0:/etc/rc.d/rc.local node$i:/home/jakub/;\
 ssh -t node$i sudo cp /home/jakub/rc.local /etc/rc.d/;\
 ssh -t node$i sudo chmod u+x /etc/rc.d/rc.local;\
 ssh -t node$i sudo reboot;\
 done
```

And to check it works when they reboot:
```
for i in {1..4};\
 do echo "now doing node$i";\
 ssh -t node$i sudo cat /sys/kernel/mm/transparent_hugepage/defrag;\
 ssh -t node$i sudo cat /sys/kernel/mm/transparent_hugepage/enabled;\
 done
 
 now doing node1
always madvise [never]
always madvise [never]
now doing node2
always madvise [never]
always madvise [never]
now doing node3
always madvise [never]
always madvise [never]
now doing node4
always madvise [never]
always madvise [never]
```

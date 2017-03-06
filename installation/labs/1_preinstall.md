# System Configuration Checks

## 1. Check vm.swappiness on all your nodes

Setting VM swappiness to 1 - using kernel newer than 2.6
```
$ echo "vm.swappiness = 1" >> /etc/sysctl.conf 
$ echo 1 > /proc/sys/vm/swappiness
```

Check swapiness level is correct:
```
$ cat /proc/sys/vm/swappiness
1
```

## 2. Show the mount attributes of all volumes
I decided to use 100 GB SSD volume for OS and 200 GB Throughput optimized HDD for data.
I use the following mount schema:
 - Whole SSD is mounted under /
 - Whole HDD is mounted under /data/hdd_0
```
$ cat /etc/fstab

...
UUID=ef6ba050-6cdc-416a-9380-c14304d0d206 /                       xfs     defaults        0 0
UUID=48bb98ef-e950-43ab-9ede-f29532f92e68 /data/hdd_0           ext4    defaults,nofail 0 2
```

I used simple default filesystem layout:
```
$ df -h

Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1      100G  4.5G   96G   5% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
/dev/xvdb       197G  2.6G  185G   2% /data/hdd_0
tmpfs           1.5G     0  1.5G   0% /run/user/1001
```

## 3. Show the reserve space of any non-root, ext-based volumes

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


## 4. Disable transparent hugepage support

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
$ for i in {1..4};\
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
$ for i in {1..4};\
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


## 5. List your network interface configuration

To list available interfaces:
```
$ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP mode DEFAULT qlen 1000
    link/ether 0a:20:d7:39:2a:8f brd ff:ff:ff:ff:ff:ff
```

Ignoring the loopback interface eth0 is the only interface I use in this setup.
To show its properties:
```
$ cat /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE="eth0"
BOOTPROTO="dhcp"
ONBOOT="yes"
TYPE="Ethernet"
USERCTL="yes"
PEERDNS="yes"
IPV6INIT="no"
PERSISTENT_DHCLIENT="1"
```

## 6. List forward and reverse host lookups using getent or nslookup

Since I use /etc/hosts file I had to use getent utility as follows:
```
# From hostname to IP:
$for i in {0..5};\
  do getent hosts node$i;\
done
 
172.31.1.215    node0.testcluster node0
172.31.15.231   node1.testcluster node1
172.31.9.230    node2.testcluster node2
172.31.15.155   node3.testcluster node3
172.31.2.140    node4.testcluster node4

# From IP to hostname:
for i in "172.31.1.215" "172.31.15.231" "172.31.9.230" "172.31.15.155" "172.31.2.140";\
  do getent hosts $i ;\
done

172.31.1.215    node0.testcluster node0
172.31.15.231   node1.testcluster node1
172.31.9.230    node2.testcluster node2
172.31.15.155   node3.testcluster node3
172.31.2.140    node4.testcluster node4
```

## 7. Show the nscd service is running

To show nscd status I used:
```
$ sudo systemctl status nscd

 nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2017-03-06 11:00:28 UTC; 3h 51min ago
 Main PID: 3866 (nscd)
   CGroup: /system.slice/nscd.service
           +-3866 /usr/sbin/nscd

```

## 8. Show the ntpd service is running
NTP is not installed on Centos 7 machine by default.
I had to install it using:
```
for i in {0..5};\
 do echo "now doing node$i";\
 ssh -t node$i sudo yum -y install ntp;\
 ssh -t node$i sudo systemctl enable ntpd;\
 ssh -t node$i sudo systemctl start ntpd;\
 ssh -t node$i sudo ntpstat;\
done
 
```

An to check taht it works I used:
```
for i in {0..5};\
  do ssh -t node$i echo "Date at node$i is:" $(date);\
done

Date at node0 is: Mon Mar 6 15:02:48 UTC 2017
Date at node1 is: Mon Mar 6 15:02:48 UTC 2017
Date at node2 is: Mon Mar 6 15:02:48 UTC 2017
Date at node3 is: Mon Mar 6 15:02:48 UTC 2017
Date at node4 is: Mon Mar 6 15:02:48 UTC 2017
```

Date seem to be the same throughout the cluster.
List the cloud provider you are using (AWS, GCE, Azure, other)
```
AWS 5x m3.xlarge instabce using centos 7 AMI from marketplace
```

List the nodes you are using by IP address and name
```
for i in "172.31.11.167" "172.31.9.63" "172.31.14.21" "172.31.6.252" "172.31.4.66";\
do \
	ssh -t -i ~/key.pem $i sudo hostname -f;\
done

ip-172-31-11-167.us-west-2.compute.internal
Connection to 172.31.11.167 closed.
ip-172-31-9-63.us-west-2.compute.internal
Connection to 172.31.9.63 closed.
ip-172-31-14-21.us-west-2.compute.internal
Connection to 172.31.14.21 closed.
ip-172-31-6-252.us-west-2.compute.internal
Connection to 172.31.6.252 closed.
ip-172-31-4-66.us-west-2.compute.internal
Connection to 172.31.4.66 closed.

```
List the Linux release you are using
```
sudo cat /etc/centos-release

CentOS Linux release 7.2.1511 (Core)
```
Demonstrate the disk capacity available on each node is >= 30 GB

```
df -h
 
 
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       80G  943M   80G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

```
List the command and output for yum repolist enabled

```
 yum repolist enabled
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirror.sigmanet.com
 * extras: mirrors.cat.pdx.edu
 * updates: mirror.scalabledns.com
repo id                                                                                               repo name                                                                                              status
!base/7/x86_64                                                                                        CentOS-7 - Base                                                                                        9,363
!extras/7/x86_64                                                                                      CentOS-7 - Extras                                                                                        311
!updates/7/x86_64                                                                                     CentOS-7 - Updates                                                                                     1,107

```



Add the following Linux accounts to all nodes
```
for i in "172.31.11.167" "172.31.9.63" "172.31.14.21" "172.31.6.252" "172.31.4.66";\
	do \
	ssh -t -i ~/key.pem $i hostname;\
	ssh -t -i ~/key.pem $i sudo useradd -u 2010 neymar;\
	ssh -t -i ~/key.pem $i sudo useradd -u 2016 ronaldo;\
	ssh -t -i ~/key.pem $i sudo groupadd barca;\
	ssh -t -i ~/key.pem $i sudo groupadd merengues;\
	ssh -t -i ~/key.pem $i sudo usermod -a -G barca ronaldo;\
	ssh -t -i ~/key.pem $i sudo usermod -a -G neymar merengues;\
done
```


List the /etc/passwd entries for neymar and ronaldo
```
sudo cat /etc/passwd | grep -e ronaldo -e neymar

neymar:x:2010:2010::/home/neymar:/bin/bash
ronaldo:x:2016:2016::/home/ronaldo:/bin/bash

```
List the /etc/group entries for barca and merengues
```
sudo cat /etc/group | grep -e barca -e merengues

barca:x:2017:ronaldo
merengues:x:2018:

```



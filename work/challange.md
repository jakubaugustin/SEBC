# Preconditions 

## Create CentOS 7.1 x86_64 with cloud-init (HVM) AMI

## IP list
```
"172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167"
```

**Copy key to machine:**
```
$ vi ~/key.pem

-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA05+GfKUgccGhIsyfI3Ygcd2LT57S9xhQ97fMFlB9aqRK0+M/
c4t1qzVa4UUhtQMCXKuD+bJ1Hc1AZuw2HTZONhX0m3qKzwEPBAgnCc+dMDvHPEo7
eUvm+oi85FzdWcE8MnD6B55FFLNcdtYpoo9/UOW7CviULjMHSQT1wp2PNaUAUgul
feUY5Aw5rKrSPLDSzR0OI9BMgMuWCJHmsFL8V9WHlk+QGQmXlUQIBwwiiFXL93qp
aN96Um46HCpOCRkH4wiJpKN6O/mfenpMenwzNujNW6lyOrMD2pL/fMOwwpdjqpnJ
gklGC/PzLX6iszp+MgFD70Wg2V6S+IkQbnMc4QIDAQABAoIBAHHlQbSECtoupFLe
Xifvw7aEzh2kFVb3t1wbh7PaziU/FybC/7toK4Rhyu/DDUkmvXayuO0CpxXLCgZa
yyUdvSpO1r93TI3su/AnkxssqiTzh19jdG7r8vyT61XcxSUxYvyi4W6IOBXUEsfC
q9XZ9WPMwMY+00GqJRmfmcWMly7/C4qoutcy3QZfaV8/aYQU/4akKSraM8g7oAnL
m5v1bust73tGD8y06LOL4u9Vty1qyxDHYtgjAQcaKeFwDIlBKXHZbkvZ4oqV8g6Z
nW0BrrdqGaIbjM1Z7qgXcB19PwoCPwQQWihFzPx3tN1P4+gRzr3Vb6shAFlEBmV2
lRl/HYECgYEA/nsffH4Ft6IRTqxPmBLzNUoKyQY++W76OX7r5PePwETQDMn03U4s
/vJw1kFqyaxot90cyE9BarHEYfkLsRUzC7wS8mDGtMj5YIdY/C6oKMMNUsddR2y4
UEPOOYd9MjDpw2X6nCZH1lEB1NDzsMBxNB/R2fBO/4r+avzvfmmRt/0CgYEA1OLp
Gdh25NHUBIA0nBcOH19k1kfBS2M5/TeFVghNK+2m0U2ttM32gtvs/EXFTIboUFi1
aX5fWDDtTnGMe6xSxonDBFPFNZg3QYeSGdfTJJKu0hua2b32jMnDB6ZUKhe8inLY
NUBeLtt8LtCiZMwiBLAz2E/IRUJ/vrQlbPlpU7UCgYEAn4iWQ5hJg0ZxrS1utHpk
x6qEOmPVBNAiw/qibacZEkLRXsMY48gHg0h/noHiLU4NU/6k9Zph+z44S+cyAjC1
EI02H4a16032sCIJkga52tv0tUlQW993aLIpTX136ggp9BoxUsTY0i10hXL84niy
PygXiZYSIDeFqZKpnUkXVg0CgYAC7hSTPH12bMTkQvd2ZoLVP7TdliM87GKx73+w
TXDyd9Th8JXBdUw9RNWgKz2p7floka/9gbXCOvopKDrswNRq0x6SAq0mLbAlAL6s
CGJpkHNDhQm+kXTBP02l304tPiJkLWx4XyhssKym4Ew74utc8SflhEOXYHDtqQES
3OPsOQKBgA1ZhV5rKpp4r/tMQ2A/VFpYWg7/XnD5GEhSvkvYAbtjvPfoprOtZ7x5
6zDT9K7LeLFVz4tzUbZp0BetlA0gfAmTBtsYVofrBgT7hp8ygzcpA34oxR4I3Dkr
NmOM3cRsKhxu5FdE0jtBt9bBmHLDYTTuIQhEL2sq4l8pPSZ00vmI
-----END RSA PRIVATE KEY-----


$ chmod 600 ~/key.pem 
```

**Check hostnames work:**
```
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
do \
	ssh -t -i ~/key.pem $i sudo hostname -f;\
done
```

Add the following to the bottom of /etc/rc.d/rc.local
```
if test -f /sys/kernel/mm/transparent_hugepage/enabled; then
echo never > /sys/kernel/mm/transparent_hugepage/enabled
fi
if test -f /sys/kernel/mm/transparent_hugepage/defrag; then
echo never > /sys/kernel/mm/transparent_hugepage/defrag
fi


Distribute rc.local	
```	
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
 do echo "now doing node$i";\
 ssh -i ~/key.pem -t $i sudo cp /etc/rc.d/rc.local ~;\
 scp -i ~/key.pem /etc/rc.d/rc.local $i:/tmp;\
 ssh -i ~/key.pem -t $i sudo cp /tmp/rc.local /etc/rc.d/;\
 ssh -i ~/key.pem -t $i sudo chmod u+x /etc/rc.d/rc.local;\
 ssh -i ~/key.pem -t $i sudo reboot;\
done
```


Enable ntp
```	
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
 do echo "now doing node$i";\
 ssh -i ~/key.pem -t $i sudo yum install -y ntp;\
 ssh -i ~/key.pem -t $i sudo systemctl enable ntpd;\
 ssh -i ~/key.pem -t $i sudo systemctl start ntpd;\
 ssh -i ~/key.pem -t $i sudo ntpstat;\
done
```

## In the file challenges/labs/0_setup.md
**List the cloud provider you are using (AWS, GCE, Azure, other):**
```
AWS, using 5x m3.xlarge instance
```

**List the Linux release you have chosen**
```
$cat /etc/centos-release

CentOS Linux release 7.1.1503 (Core)
```

**Show that the disk space on each node is at least 30 GB**
```
$ df -h

Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       30G  867M   30G   3% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G  8.3M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
```

**List the command and output for yum repolist enabled**
```
$ sudo yum repolist enabled

repo id                                                                                repo name                                                                                                             status
base/7/x86_64                                                                          CentOS-7 - Base                                                                                                        9,363
epel/x86_64                                                                            Extra Packages for Enterprise Linux 7 - x86_64                                                                        11,307
extras/7/x86_64                                                                        CentOS-7 - Extras                                                                                                        310
updates/7/x86_64                                                                       CentOS-7 - Updates                                                                                                     1,107
repolist: 22,087
```


**Add the following Linux accounts to all nodes**

```
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
	do \
	ssh -t -i ~/key.pem $i hostname;\
	ssh -t -i ~/key.pem $i sudo useradd -u 2000 raffles;\
	ssh -t -i ~/key.pem $i sudo useradd -u 3000 fullerton;\
	ssh -t -i ~/key.pem $i sudo groupadd hotels;\
	ssh -t -i ~/key.pem $i sudo groupadd shops;\
	ssh -t -i ~/key.pem $i sudo usermod -a -G hotels fullerton;\
	ssh -t -i ~/key.pem $i sudo usermod -a -G shops raffles;\
done
```

## Set swappiness level
```
for i in "172.31.6.106" "172.31.0.202" "172.31.15.74" "172.31.7.221" "172.31.12.209";\
do\
 ssh -i ~/key.pem -t $i sudo -u root echo "vm.swappiness = 1" >> /etc/sysctl.conf ;\
 ssh -i ~/key.pem -t $i sudo -u root echo 1 > /proc/sys/vm/swappiness;\
 ssh -i ~/key.pem -t $i sudo reboot;\
done

```

# MariaDB

## 1. Adding the repository

Firstly I created empty MariaDB repository to yum:
```
sudo vi /etc/yum.repos.d/mariadb.repo
```

I added the following information to newly created file (RHEL7 MariaDB repo):
```
# MariaDB 10.1 CentOS repository list - created 2016-11-30 16:07 UTC 
# http://downloads.mariadb.org/mariadb/repositories/ 
[mariadb] 
name = MariaDB 
baseurl = http://yum.mariadb.org/10.1/centos7-amd64 
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB 
gpgcheck=1
```

Refresh the yum cache
```
sudo yum clean all
```
# 2. Installing the MariaDB server

Installing the MariaDB server on node0 and node1.
Enabling it to start after reboot and starting it.

```
yum -y install MariaDB-server
sudo systemctl enable mariadb.service
sudo systemctl start mariadb.service
```
# 3. Configuring the MariaDB server

Runnig initial setup
```
$ sudo /usr/bin/mysql_secure_installation

[...]
Enter current password for root (enter for none):
OK, successfully used password, moving on...
[...]
Set root password? [Y/n] y
New password:
Re-enter new password:
Remove anonymous users? [Y/n] Y
[...]
Disallow root login remotely? [Y/n] N
[...]
Remove test database and access to it [Y/n] Y
[...]
Reload privilege tables now? [Y/n] Y
All done!
```

## Mysql create databases
```
create database amon DEFAULT CHARACTER SET utf8;
grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'password_for_amon';

create database rman DEFAULT CHARACTER SET utf8;
grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'password_for_rman';

create database metastore DEFAULT CHARACTER SET utf8;
grant all on metastore.* TO 'hive'@'%' IDENTIFIED BY 'password_for_hive';

create database sentry DEFAULT CHARACTER SET utf8;
grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'password_for_sentry';

create database nav DEFAULT CHARACTER SET utf8;
grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'password_for_nav';

create database navms DEFAULT CHARACTER SET utf8;
grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'password_for_navms';

create database hue DEFAULT CHARACTER SET utf8;
grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'password_for_hue';

create database oozie DEFAULT CHARACTER SET utf8;
grant all on oozie.* TO 'oozie'@'%' IDENTIFIED BY 'password_for_oozie';
```

# Install CM

## Adding repo files
On node0 I added the following file:
```
sudo vi /etc/yum.repos.d/cm.repo
```

I added the following to that file:
```
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.8.3/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1
```

to distribute it to other hosts I used:
```
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
	do \
	ssh -t -i ~/key.pem $i hostname;\
	scp -i ~/key.pem /etc/yum.repos.d/cm.repo $i:/tmp;\
	ssh -t -i ~/key.pem $i sudo cp /tmp/cm.repo /etc/yum.repos.d\;
	ssh -t -i ~/key.pem $i sudo yum clean all\;
done
```


## Installing Java
Next I installed java to all hosts:
```
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
	do \
	ssh -t -i ~/key.pem $i sudo yum -y install oracle-j2sdk1.7;\
done
```

Next download jdbc driver
```
sudo yum -y install wget
wget "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.41.tar.gz" -P ~
```

Now extract and copy JDBC driver to java location
```
sudo mkdir /usr/share/java
sudo tar zxvf mysql-connector-java-5.1.41.tar.gz
sudo cp mysql-connector-java-5.1.41/mysql-connector-java-5.1.41-bin.jar /usr/share/java/mysql-connector-java.jar
```

Next distribute JDBC driver
```
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
	do \
	scp -i ~/key.pem /usr/share/java/mysql-connector-java.jar $i:/tmp;\
	ssh -t -i ~/key.pem $i sudo mkdir -p /usr/share/java\;
	ssh -t -i ~/key.pem $i sudo cp /tmp/mysql-connector-java.jar /usr/share/java;\
done
```


Install CM server
```
sudo yum install -y cloudera-manager-daemons cloudera-manager-server
sudo systemctl enable cloudera-scm-server
sudo /usr/share/cmf/schema/scm_prepare_database.sh -uroot -pcloudera mysql scm scm

sude systemctl start clouderascm-server

```

Create hdfs users:
```
sudo -u hdfs hadoop fs -mkdir /user/raffles
sudo -u hdfs hadoop fs -chown raffles:raffles /user/raffles

sudo -u hdfs hadoop fs -mkdir /user/fullerton
sudo -u hdfs hadoop fs -chown fullerton:fullerton /user/fullerton
```


Run teragen
```
time sudo -u raffles yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen\
 -Dmapred.map.tasks=6\
 -Ddfs.block.size=33554432\
 52000000\
 /user/raffles/teragen512m
 
hdfs fs -ls /user/raffles/teragen512m

hdfs fsck /user/raffles/teragen512m -files -blocks
```

# Kerberize cluster

## Install kerberos for master node

```
sudo yum -y install krb5-server krb5-libs krb5-auth-dialog krb5-workstation
```

```
for i in "172.31.2.124" "172.31.15.80" "172.31.4.183" "172.31.15.21" "172.31.9.167";\
 do echo "now doing $i";\
 ssh -i ~/key.pem -t $i sudo yum -y install krb5-workstation krb5-libs krb5-auth-dialog;\
done
```
 
## Run tests
  
```
 time  yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen\
 -Dmapred.map.tasks=4\
 -Ddfs.block.size=33554432\
 52000000\
 /user/raffles/teragen512
```

```
  time  yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar pi 10 100\
```

#Sentry and beeline

## connect command
```
	
```
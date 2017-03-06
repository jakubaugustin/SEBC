# 1. Adding cloudera repo file

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
for i in {1..4};\
	do scp /etc/yum.repos.d/cm.repo node$i:/home/jakub/;\
	ssh -t node$i sudo cp /home/jakub/cm.repo /etc/yum.repos.d\;
	ssh -t node$i sudo yum clean all\;
done
```

# 2. Installing Java
Next I installed java to all hosts:
```
for i in {0..4};\
	do ssh -t node$i sudo yum -y install oracle-j2sdk1.7;\
done
```

Now extract and copy JDBC driver to java location
```
sudo mkdir /usr/share/java
sudo tar zxvf mysql-connector-java-5.1.40.tar.gz
sudo cp mysql-connector-java-5.1.41/mysql-connector-java-5.1.41-bin.jar /usr/share/java/mysql-connector-java.jar
```


# 3. Installing Cloudera Manager

I picked node0 as my edge server and installed cloudera manager there:
```
sudo yum install cloudera-manager-daemons cloudera-manager-server
```


Next allow cloudera-scm-server to start after reboot
```
sudo systemctl enable cloudera-scm-server
```


Prepare MariaDB databse for SCM

```
$ /usr/share/cmf/schema/scm_prepare_database.sh -uroot -p<mypassword> mysql scm scm
Enter SCM password:

JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```

And start Cloudera SCM Server:
```
sudo systemctl start cloudera-scm-server	
```
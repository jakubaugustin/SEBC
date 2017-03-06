#Installing MariDB

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
for i in {0..1};\
	do ssh -t node$i sudo yum -y install MariaDB-server;\
	ssh -t node$i sudo systemctl enable mariadb.service;\
	ssh -t node$i sudo systemctl start mariadb.service;\
done
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

Next download the JDBCclient from https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.41.tar.gz
I downloaded client to all machines (for now to my home ditectory - I will copy it to java dir when it is installed)

```
wget "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.41.tar.gz" -P /home/jakub/
```

Next I did som tweaking to MariaDB conf.
I create new file: /etc/my.conf.d/lab.cnf

```
sudo vi /etc/my.conf.d/lab.cnf
```
I used the following configuration for both hosts:

```
[mysqld]
transaction-isolation = READ-COMMITTED

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1

max_connections = 500
expire_logs_days = 10

log_bin=/var/lib/mysql/mysql_binary_log

binlog_format = row

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M
```

# 4. Creating databases

Creating database for Activity Monitor
```
mysql> create database amon DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'password_for_amon';
Query OK, 0 rows affected (0.00 sec)
```

Creating database for Reports Manager
```
mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'password_for_rman';
Query OK, 0 rows affected (0.00 sec)
```

Creating database for Hive Metastore Server
```
mysql> create database metastore DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on metastore.* TO 'hive'@'%' IDENTIFIED BY 'password_for_hive';
Query OK, 0 rows affected (0.00 sec)
```

Creating database for Sentry Server
```
mysql> create database sentry DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'password_for_sentry';
Query OK, 0 rows affected (0.00 sec)
```

Creating database for Cloudera Navigator Audit Server
```
mysql> create database nav DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'password_for_nav';
Query OK, 0 rows affected (0.00 sec)
```

Creating database for Cloudera Navigator Metadata Server
```
mysql> create database navms DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'password_for_navms';
Query OK, 0 rows affected (0.00 sec)
```

Creating database for Hue
```
mysql> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'password_for_hue';
Query OK, 0 rows affected (0.00 sec)
```
Creating database for Oozie server
```
mysql> create database oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on oozie.* TO 'oozie'@'%' IDENTIFIED BY 'password_for_oozie';
Query OK, 0 rows affected (0.00 sec)
```

# 5. Enabling Galera cluster
On node0 id added the following to /etc/my.cnf.d/lab.cnf:
```
# Galera Provider Configuration
wsrep_on=ON
wsrep_provider=/usr/lib64/galera/libgalera_smm.so

# Galera Cluster Configuration
wsrep_cluster_name="cebsMariaCluster"
wsrep_cluster_address="gcomm://"

# Galera Synchronization Congifuration
wsrep_sst_method=rsync

# Galera Node Configuration
wsrep_node_address="172.31.1.215"
wsrep_node_name="node0"
```

On node2 I added the following to /etc/my.cnf.d/lab.cnf:
```
# Galera Provider Configuration
wsrep_on=ON
wsrep_provider=/usr/lib64/galera/libgalera_smm.so

# Galera Cluster Configuration
wsrep_cluster_name="cebsMariaCluster"
wsrep_cluster_address="gcomm://172.31.1.215"

# Galera Synchronization Congifuration
wsrep_sst_method=rsync

# Galera Node Configuration
wsrep_node_address="172.31.15.231"
wsrep_node_name="node1"
```

Next I restarted both servers using:

```
sudo systemctl restart mariadb.service
```

I had to create inbound security rules for ports: 4444, 4567, 4568, 3306 for Galera to work.

Then when I run show databases on node1 I see the list even though I created those databases on node0.

To double check that Galera replication works I connected to mysql and ran:
```
SHOW GLOBAL STATUS LIKE 'wsrep_%';

+------------------------------+--------------------------------------+
| Variable_name                | Value                                |
+------------------------------+--------------------------------------+
| wsrep_apply_oooe             | 0.000000                             |
| wsrep_apply_oool             | 0.000000                             |
| wsrep_apply_window           | 0.000000                             |
| wsrep_causal_reads           | 0                                    |
| wsrep_cert_deps_distance     | 0.000000                             |
| wsrep_cert_index_size        | 0                                    |
| wsrep_cert_interval          | 0.000000                             |
| wsrep_cluster_conf_id        | 2                                    |
| wsrep_cluster_size           | 2                                    |
| wsrep_cluster_state_uuid     | 6f49f7d0-0286-11e7-815b-7e36bbb61894 |
| wsrep_cluster_status         | Primary                              |
| wsrep_commit_oooe            | 0.000000                             |
| wsrep_commit_oool            | 0.000000                             |
| wsrep_commit_window          | 0.000000                             |
| wsrep_connected              | ON                                   |
| wsrep_desync_count           | 0                                    |
| wsrep_evs_delayed            |                                      |
| wsrep_evs_evict_list         |                                      |
| wsrep_evs_repl_latency       | 0/0/0/0/0                            |
| wsrep_evs_state              | OPERATIONAL                          |
| wsrep_flow_control_paused    | 0.000000                             |
| wsrep_flow_control_paused_ns | 0                                    |
| wsrep_flow_control_recv      | 0                                    |
| wsrep_flow_control_sent      | 0                                    |
| wsrep_gcomm_uuid             | bae8127c-0287-11e7-b34c-93277fe76bc5 |
| wsrep_incoming_addresses     | 172.31.1.215:3306,172.31.15.231:3306 |
| wsrep_last_committed         | 0                                    |
| wsrep_local_bf_aborts        | 0                                    |
| wsrep_local_cached_downto    | 18446744073709551615                 |
| wsrep_local_cert_failures    | 0                                    |
| wsrep_local_commits          | 0                                    |
| wsrep_local_index            | 1                                    |
| wsrep_local_recv_queue       | 0                                    |
| wsrep_local_recv_queue_avg   | 0.000000                             |
| wsrep_local_recv_queue_max   | 1                                    |
| wsrep_local_recv_queue_min   | 0                                    |
| wsrep_local_replays          | 0                                    |
| wsrep_local_send_queue       | 0                                    |
| wsrep_local_send_queue_avg   | 0.000000                             |
| wsrep_local_send_queue_max   | 1                                    |
| wsrep_local_send_queue_min   | 0                                    |
| wsrep_local_state            | 4                                    |
| wsrep_local_state_comment    | Synced                               |
| wsrep_local_state_uuid       | 6f49f7d0-0286-11e7-815b-7e36bbb61894 |
| wsrep_protocol_version       | 7                                    |
| wsrep_provider_name          | Galera                               |
| wsrep_provider_vendor        | Codership Oy <info@codership.com>    |
| wsrep_provider_version       | 25.3.19(r3667)                       |
| wsrep_ready                  | ON                                   |
| wsrep_received               | 3                                    |
| wsrep_received_bytes         | 219                                  |
| wsrep_repl_data_bytes        | 0                                    |
| wsrep_repl_keys              | 0                                    |
| wsrep_repl_keys_bytes        | 0                                    |
| wsrep_repl_other_bytes       | 0                                    |
| wsrep_replicated             | 0                                    |
| wsrep_replicated_bytes       | 0                                    |
| wsrep_thread_count           | 2                                    |
+------------------------------+--------------------------------------+
```
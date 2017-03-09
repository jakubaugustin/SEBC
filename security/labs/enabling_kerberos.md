Install open LDAP clients

```
sudo yum -y install openldap-clients
```

Install Kerberos server
```
sudo yum -y install krb5-server krb5-libs krb5-auth-dialog krb5-workstation
```

Install kerberos clients on ALL hosts
```
for i in {0..4};\
	do ssh -t node$i sudo yum -y install krb5-workstation krb5-libs krb5-auth-dialog;\
done
```

Set kdc.conf file
```
$ sudo vim /var/kerberos/krb5kdc/kdc.conf

[kdcdefaults]
 kdc_ports = 88
 kdc_tcp_ports = 88

[realms]
 TESTCLUSTER.COM = {
  #master_key_type = aes256-cts
  acl_file = /var/kerberos/krb5kdc/kadm5.acl
  dict_file = /usr/share/dict/words
  admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
  supported_enctypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal des-hmac-sha1:normal des-cbc-md5:normal des-cbc-crc:normal
  max_life = 1d
  max_renewable_life = 7d
 }

```


```
$sudo vi /etc/krb5.conf

# Configuration snippets may be placed in this directory as well
includedir /etc/krb5.conf.d/

[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
default_realm = TESTCLUSTER.COM
dns_lookup_kdc = false
dns_lookup_realm = false
ticket_lifetime = 86400
renew_lifetime = 604800
forwardable = true
default_tgs_enctypes = des3-hmac-sha1 aes256-cts aes128-cts arcfour-hmac des-hmac-sha1 des-cbc-md5 des-cbc-crc
default_tkt_enctypes = des3-hmac-sha1 aes256-cts aes128-cts arcfour-hmac des-hmac-sha1 des-cbc-md5 des-cbc-crc
permitted_enctypes = des3-hmac-sha1 aes256-cts aes128-cts arcfour-hmac des-hmac-sha1 des-cbc-md5 des-cbc-crc
udp_preference_limit = 1

[realms]
TESTCLUSTER.COM = {
kdc = node0.testcluster
admin_server = node0.testcluster
}

```

```
for i in {1..4};\
 do scp /etc/krb5.conf node$i:/home/jakub/;\
 ssh -t node$i sudo mv /home/jakub/krb5.conf /etc/;\
done
```



create kerberos database

```
/usr/sbin/kdb5_util create -s

[cloudera]
```

Add cloudera principal
```
sudo kadmin.local

addprinc cloudera-scm

WARNING: no policy specified for cloudera-scm@TESTCLUSTER.COM; defaulting to no policy
Enter password for principal "cloudera-scm@TESTCLUSTER.COM":
Re-enter password for principal "cloudera-scm@TESTCLUSTER.COM":
Principal "cloudera-scm@TESTCLUSTER.COM" created.
```

Add cloudera-scm to /admin
```
sudo vim /var/kerberos/krb5kdc/kadm5.acl

*/admin@TESTCLUSTER.COM *
cloudera-scm@TESTCLUSTER.COM admilc
```

```
$ sudo kadmin.local
kadmin.local:  addpol admin
kadmin.local:  addpol users
kadmin.local:  addpol hosts
kadmin.local:  exit
```


```
sudo systemctl enable krb5kdc
sudo systemctl enable kadmin 

sudo systemctl restart krb5kdc
sudo systemctl restart kadmin 
```



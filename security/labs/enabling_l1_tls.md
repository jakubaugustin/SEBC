```
$ sudo mkdir -p /opt/cloudera/security/x509/ /opt/cloudera/security/jks/
```

```
$ cd /opt/cloudera/security/jks
```

```
$ sudo chown -R cloudera-scm:cloudera-scm /opt/cloudera/security/jks
```

```
$ sudo /usr/java/jdk1.7.0_67-cloudera/bin/keytool -genkeypair -keystore example.keystore -keyalg RSA -alias cmhost \
-dname "CN=ip-172-31-1-215,OU=us-west-2,OU=compute,OU=internal" -storepass cloudera -keypass cloudera
```

```
$ export JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera/
```

```
$ sudo cp $JAVA_HOME/jre/lib/security/cacerts $JAVA_HOME/jre/lib/security/jssecacerts
```

```
$ sudo /usr/java/jdk1.7.0_67-cloudera/bin/keytool -export -alias cmhost -keystore example.keystore -rfc -file selfsigned.cer

[cloudera]

Certificate stored in file <selfsigned.cer>
```

```
$ sudo cp selfsigned.cer /opt/cloudera/security/x509/cmhost.pem
```

```
$ sudo /usr/java/jdk1.7.0_67-cloudera/bin/keytool -import -alias cmhost -file /opt/cloudera/security/jks/selfsigned.cer \
-keystore $JAVA_HOME/jre/lib/security/jssecacerts -storepass changeit

Owner: CN=node0.testcluster, OU=testcluster
Issuer: CN=node0.testcluster, OU=testcluster
Serial number: 5a277985
Valid from: Wed Mar 08 14:10:47 UTC 2017 until: Tue Jun 06 14:10:47 UTC 2017
Certificate fingerprints:
         MD5:  9B:DF:24:CB:A4:23:08:F5:AB:8B:CE:85:54:BD:9B:65
         SHA1: 12:B9:97:D8:6B:32:65:3C:5F:1C:BB:C3:A3:A5:B1:18:41:5D:72:8C
         SHA256: D9:4B:91:A1:BE:CA:F1:1F:DB:9E:BF:38:D0:0C:B6:46:07:23:7E:79:B7:CF:65:03:3E:7E:DB:D9:52:96:8D:55
         Signature algorithm name: SHA256withRSA
         Version: 3

Extensions:

#1: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 99 3D 6F 2A FA 9E 52 4A   20 3A 4A D3 C9 E9 7A 09  .=o*..RJ :J...z.
0010: 44 AD 9A 8A                                        D...
]
]

Trust this certificate? [no]:  yes
Certificate was added to keystore/
```

```
for i in {1..4};\
 do ssh -t node$i sudo mkdir -p /opt/cloudera/security/jks/;\
 scp /opt/cloudera/security/jks/selfsigned.cer node$i:/home/jakub/;\
 ssh -t node$i sudo cp /home/jakub/selfsigned.cer /opt/cloudera/security/jks/;\
 ssh -t node$i sudo chown -R cloudera-scm:cloudera-scm /opt/cloudera/security/jks;\
 ssh -t node$i sudo /usr/java/jdk1.7.0_67-cloudera/bin/keytool -import -alias cmhost2 -file /opt/cloudera/security/jks/selfsigned.cer \
   -keystore /usr/java/jdk1.7.0_67-cloudera/jre/lib/security/jssecacerts -storepass changeit;\
done
```

```
$ sudo mv /opt/cloudera/security/jks/example.keystore /opt/cloudera/security/jks/cmhost-keystore.jks
```

For cloudera management service change TLS/SSL Client Truststore File Location to: /usr/java/jdk1.7.0_67-cloudera/jre/lib/security/jssecacerts and Cloudera Manager Server TLS/SSL Certificate Trust Store Password to: changeit
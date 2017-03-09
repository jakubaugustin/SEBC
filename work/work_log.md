# SEBC work log

## VM swappiness

Setting VM swappiness to 1 - using kernel newer than 2.6
```
$ echo "vm.swappiness = 1" >> /etc/sysctl.conf 
$ echo 1 > /proc/sys/vm/swappiness
```

Check swapiness level
```
$ cat /proc/sys/vm/swappiness
```

## Disabling transparent hugepages on Centos 7
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


## Installing NTP
Install NTP
```
$ sudo yum -y install ntp
```

Enable NTP
```
$ sudo systemctl enable ntpd
```

Start NTP deamon
```
$ sudo systemctl start ntpd
```

Check that NTP workd
```
$ ntpstat
```
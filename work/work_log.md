Disabling transparent hugepages on Centos 7
```
$ cat /sys/kernel/mm/transparent_hugepage/defrag
$ cat /sys/kernel/mm/transparent_hugepage/enabled
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
To verfiy if THP is disabled.
```
$ cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]
$ cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
```
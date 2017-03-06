# Creating custom parcel repository from CM erver

## Installing HTTPD
```
$ sudo yum -y install httpd
```

Enable and start httpd service:
```
$ sudo systemctl enable httpd
$ sudo systemctl start httpd
```

## Configuring web server to host parcel files

Make directory to web serve`s root dir:
```
 sudo mkdir -p /var/www/html/parcels/5.8.3
 ```
 
## Downloading files for repository
 
 Download parcel files to specified directory:
 ```
 cd /var/www/html/parcels/5.8.3/
 sudo wget http://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel
 sudo wget http://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1
 sudo wget http://archive.cloudera.com/cdh5/parcels/5.8.3/manifest.json
 sudo chmod 755 ./*
 ```
 
 
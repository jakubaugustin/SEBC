## Report the latest available version of the API
```
http://35.163.17.217:7180/api/version

v15
```

## Report the CM version
```
http://35.163.17.217:7180/api/v15/cm/version

{
  "version" : "5.10.0",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20170120-1037",
  "gitHash" : "aa0b5cd5eceaefe2f971c13ab657020d96bb842a",
  "snapshot" : false
}
```
## List all CM users
```
http://35.163.17.217:7180/api/v15/users

{
  "items" : [ {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "jakubaugustin",
    "roles" : [ "ROLE_ADMIN" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  } ]
}
```
## Report the database server in use by CM
```
http://35.163.17.217:7180/api/v15/cm/scmDbInfo

{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```
# CM Treasure Hun
## What is ubertask optimization?
Running MapReduce application directly in ApplicationManager.
This may provide performance boost for smaller jobs that can fit into single container. (Some larger jobs may fail for lack of resources in this mode).
Extra overhead of requeting containers from YARN for mappers and reducers is eliminated while using uber mode. 

## Where in CM is the Kerberos Security Realm value displayed?
Administration > Settings > Kerberos > Kerberos Security Realm (default_realm)

## Which CDH service(s) host a property for enabling Kerberos authentication?
- **Hadoop HDFS:** hadoop.security.authentication
- **HBase:** hbase.security.authentication
- **SOLR:** Solr Secure Authentication

*Other services (i.e. YARN) have a property to enable Kerberos authentication fow web UIs*
*All services need to have kerberos principal information to work in kerberized cluster*

## How do you upgrade the CM agents?
Either using CM upgrade wizard after upgrading the CM server or manually using yum upgrade cloudera-manager-agent or manually via tarballs.

## Give the tsquery statement used to chart Hue's CPU utilization?
select cpu_system_rate + cpu_user_rate where category=ROLE and serviceName="HUE"

## Name all the roles that make up the Hive service
- Hive Metastore Server
- WebHCatat Server
- HiveServer2
- Gateway


## What steps must be completed before integrating Cloudera Manager with Kerberos?

- Deploy MIT KDC or Active Directory Kerberos implementation to at leas on host
- Deploy Kerberos clients to all hosts
- Add Kerberos principal for Cloudera Manager Server
- Configure the KDC to allow renewable tickets with non-zero ticket lifetimes.
- Install the JCE Policy File when using AES-256 Encryption
- Make sure krb5.conf is deployed on all hosts and is configured propperly
- Import Kerberos credentials to Cloudera Manager

# MariaDB on Amazon RDS<a name="CHAP_MariaDB"></a>

Amazon RDS supports DB instances running several versions of MariaDB\. You can use the following major versions: 
+ MariaDB 10\.6
+ MariaDB 10\.5
+ MariaDB 10\.4
+ MariaDB 10\.3
+ MariaDB 10\.2

For more information about minor version support, see [MariaDB on Amazon RDS versions](#MariaDB.Concepts.VersionMgmt)\. 

You first use the Amazon RDS management tools or interfaces to create a MariaDB DB instance\. You can then use the Amazon RDS tools to perform management actions for the DB instance, such as reconfiguring or resizing the DB instance, authorizing connections to the DB instance, creating and restoring from backups or snapshots, creating Multi\-AZ secondaries, creating read replicas, and monitoring the performance of the DB instance\. You use standard MariaDB utilities and applications to store and access the data in the DB instance\. 

MariaDB is available in all of the AWS Regions\. For more information about AWS Regions, see [Regions, Availability Zones, and Local Zones](Concepts.RegionsAndAvailabilityZones.md)\. 

You can use Amazon RDS for MariaDB databases to build HIPAA\-compliant applications\. You can store healthcare\-related information, including protected health information \(PHI\), under a Business Associate Agreement \(BAA\) with AWS\. For more information, see [HIPAA compliance](http://aws.amazon.com/compliance/hipaa-compliance/)\. AWS Services in Scope have been fully assessed by a third\-party auditor and result in a certification, attestation of compliance, or Authority to Operate \(ATO\)\. For more information, see [AWS services in scope by compliance program](http://aws.amazon.com/compliance/services-in-scope/)\. 

Before creating your first DB instance, you should complete the steps in the setting up section of this guide\. For more information, see [Setting up for Amazon RDS](CHAP_SettingUp.md)\. 

## Common management tasks for MariaDB on Amazon RDS<a name="MariaDB.Concepts.General"></a>

The following are the common management tasks you perform with an Amazon RDS DB instance running MariaDB, with links to relevant documentation for each task\. 


****  

| Task area | Relevant documentation | 
| --- | --- | 
|  **Instance Classes, Storage, and PIOPS** If you are creating a DB instance for production purposes, you should understand how instance classes, storage types, and Provisioned IOPS work in Amazon RDS\.   |  [DB instance classes](Concepts.DBInstanceClass.md) [Amazon RDS storage types](CHAP_Storage.md#Concepts.Storage)  | 
|  **Multi\-AZ Deployments** Provide high availability with synchronous standby replication in a different Availability Zone, automatic failover, fault tolerance for DB instances using Multi\-AZ deployments, and read replicas\.   |  [Multi\-AZ deployments for high availability](Concepts.MultiAZ.md)  | 
|  **Amazon Virtual Private Cloud \(VPC\)** If your AWS account has a default VPC, then your DB instance is automatically created inside the default VPC\. If your account does not have a default VPC, and you want the DB instance in a VPC, you must create the VPC and subnet groups before you create the DB instance\.   |  [Determining whether you are using the EC2\-VPC or EC2\-Classic platform](USER_VPC.FindDefaultVPC.md) [Working with a DB instance in a VPC](USER_VPC.WorkingWithRDSInstanceinaVPC.md)  | 
|  **Security Groups** By default, DB instances are created with a firewall that prevents access to them\. You therefore must create a security group with the correct IP addresses and network configuration to access the DB instance\. The security group you create depends on what Amazon EC2 platform your DB instance is on, and whether you access your DB instance from an Amazon EC2 instance\.   In general, if your DB instance is on the *EC2\-Classic* platform, you will need to create a DB security group; if your DB instance is on the *EC2\-VPC* platform, you will need to create a VPC security group\.   |  [Determining whether you are using the EC2\-VPC or EC2\-Classic platform](USER_VPC.FindDefaultVPC.md) [Controlling access with security groups](Overview.RDSSecurityGroups.md)   | 
|  **Parameter Groups** If your DB instance is going to require specific database parameters, you should create a parameter group before you create the DB instance\.   |  [Working with DB parameter groups](USER_WorkingWithParamGroups.md)  | 
|  **Importing and Exporting Data** Establish procedures for importing or exporting data\.   |  [Importing data into a MariaDB DB instance](MariaDB.Procedural.Importing.md)  | 
|  **Replication** You can offload read traffic from your source MariaDB DB instance by creating read replicas\.   |  [Working with read replicas](USER_ReadRepl.md)  | 
|  **Connecting to Your DB Instance** Connect to your DB instance using a standard SQL client application\.   |  [Connecting to a DB instance running the MariaDB database engine](USER_ConnectToMariaDBInstance.md)  | 
|  **Backup and Restore** When you create your DB instance, you can configure it to take automated backups\. You can also back up and restore your databases manually by using full backup files \(\.bak files\)\.   |  [Working with backups](USER_WorkingWithAutomatedBackups.md)  | 
|  **Monitoring** Monitor your MariaDB DB instance by using Amazon CloudWatch RDS metrics, events, and Enhanced Monitoring\. View log files for your MariaDB DB instance\.   |  [Viewing metrics in the Amazon RDS console](USER_Monitoring.md) [Viewing Amazon RDS events](USER_ListEvents.md)  | 
|  **Log Files** You can access the log files for your MariaDB DB instance\.   |  [Monitoring Amazon RDS log files](USER_LogAccess.md) [MariaDB database log files](USER_LogAccess.Concepts.MariaDB.md)  | 

There are also advanced administrative tasks for working with DB instances running MariaDB\. For more information, see the following documentation: 
+ [Parameters for MariaDB](Appendix.MariaDB.Parameters.md)
+ [MariaDB on Amazon RDS SQL reference](Appendix.MariaDB.SQLRef.md)

## MariaDB on Amazon RDS versions<a name="MariaDB.Concepts.VersionMgmt"></a>

For MariaDB, version numbers are organized as version X\.Y\.Z\. In Amazon RDS terminology, X\.Y denotes the major version, and Z is the minor version number\. For Amazon RDS implementations, a version change is considered major if the major version number changes, for example going from version 10\.4 to 10\.5\. A version change is considered minor if only the minor version number changes, for example going from version 10\.3\.20 to 10\.3\.23\. 

Amazon RDS currently supports the following versions of MariaDB: 


****  

| Major version | Minor version | 
| --- | --- | 
| MariaDB 10\.6 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html)  | 
| MariaDB 10\.5 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html)  | 
| MariaDB 10\.4 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html)  | 
| MariaDB 10\.3 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html)  | 
| MariaDB 10\.2 |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html)  | 

You can specify any currently supported MariaDB version when creating a new DB instance\. You can specify the major version \(such as MariaDB 10\.5\), and any supported minor version for the specified major version\. If no version is specified, Amazon RDS defaults to a supported version, typically the most recent version\. If a major version is specified but a minor version is not, Amazon RDS defaults to a recent release of the major version you have specified\. To see a list of supported versions, as well as defaults for newly created DB instances, use the [https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-engine-versions.html](https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-engine-versions.html) AWS CLI command\.

The default MariaDB version might vary by AWS Region\. To create a DB instance with a specific minor version, specify the minor version during DB instance creation\. You can determine the default minor version for an AWS Region using the following AWS CLI command:

```
aws rds describe-db-engine-versions --default-only --engine mariadb --engine-version major-engine-version --region region --query "*[].{Engine:Engine,EngineVersion:EngineVersion}" --output text
```

Replace *major\-engine\-version* with the major engine version, and replace *region* with the AWS Region\. For example, the following AWS CLI command returns the default MariaDB minor engine version for the 10\.5 major version and the US West \(Oregon\) AWS Region \(us\-west\-2\):

```
aws rds describe-db-engine-versions --default-only --engine mariadb --engine-version 10.5 --region us-west-2 --query "*[].{Engine:Engine,EngineVersion:EngineVersion}" --output text
```

## MariaDB feature support on Amazon RDS<a name="MariaDB.Concepts.FeatureSupport"></a>

In the following sections, find MariaDB feature support on Amazon RDS for MariaDB major versions:

**Topics**
+ [MariaDB 10\.6 support on Amazon RDS](#MariaDB.Concepts.FeatureSupport.10-6)
+ [MariaDB 10\.5 support on Amazon RDS](#MariaDB.Concepts.FeatureSupport.10-5)
+ [MariaDB 10\.4 support on Amazon RDS](#MariaDB.Concepts.FeatureSupport.10-4)
+ [MariaDB 10\.3 support on Amazon RDS](#MariaDB.Concepts.FeatureSupport.10-3)
+ [MariaDB 10\.2 support on Amazon RDS](#MariaDB.Concepts.FeatureSupport.10-2)

For information about supported minor versions of Amazon RDS for MariaDB, see [MariaDB on Amazon RDS versions](#MariaDB.Concepts.VersionMgmt)\.

### MariaDB 10\.6 support on Amazon RDS<a name="MariaDB.Concepts.FeatureSupport.10-6"></a>

Amazon RDS supports the following new features for your DB instances running MariaDB version 10\.6 or later: 
+ **MyRocks storage engine** – You can use the MyRocks storage engine with RDS for MariaDB to optimize storage consumption of your write\-intensive, high\-performance web applications\. For more information, see [Supported storage engines for MariaDB on Amazon RDS](#MariaDB.Concepts.Storage) and [MyRocks](https://mariadb.com/kb/en/myrocks/)\.
+ **IAM DB authentication** – You can use IAM DB authentication for better security and central management of connections to your MariaDB DB instances\. For more information, see [IAM database authentication for MariaDB, MySQL, and PostgreSQL](UsingWithRDS.IAMDBAuth.md)\. 
+ **Upgrade options** – You can now upgrade to RDS for MariaDB version 10\.6 from any prior major release \(10\.2, 10\.3, 10\.4, 10\.5\)\. You can also take a snapshot of an existing MySQL 5\.6 or 5\.7 DB instance and restore the snapshot to a MariaDB 10\.6 instance\. For more information, see [Upgrading the MariaDB DB engine](USER_UpgradeDBInstance.MariaDB.md)\.
+ **Delayed replication** – You can now set a configurable time period for which a read replica lags behind the source database\. In a standard MariaDB replication configuration, there is minimal replication delay between the source and the replica\. With delayed replication, you can set an intentional delay as a strategy for disaster recovery\. For more information, see [Configuring delayed replication with MariaDB](USER_MariaDB.Replication.ReadReplicas.md#USER_MariaDB.Replication.ReadReplicas.DelayReplication)\.
+ **Oracle PL/SQL compatibility** – By using RDS for MariaDB version 10\.6, you can more easily migrate your legacy Oracle applications to Amazon RDS\. For more information, see [SQL\_MODE=ORACLE](https://mariadb.com/kb/en/sql_modeoracle/)\.
+ **Atomic DDL** – Your dynamic data language \(DDL\) statements can be relatively crash\-safe with RDS for MariaDB version 10\.6\. `CREATE TABLE`, `ALTER TABLE`, `RENAME TABLE`, `DROP TABLE`, `DROP DATABASE` and related DDL statements are now atomic\. Either the statement succeeds, or it's completely reversed\. For more information, see [Atomic DDL](https://mariadb.com/kb/en/atomic-ddl/)\.
+ **Other enhancements** – These enhancements include a `JSON_TABLE` function for transforming JSON data to relational format within SQL, and faster empty table data load with Innodb\. They also include new `sys_schema` for analysis and troubleshooting, optimizer enhancement for ignoring unused indexes, and performance improvements\. For more information, see [JSON\_TABLE](https://mariadb.com/kb/en/json_table/)\.
+ **New default values for parameters** – The following parameters have new default values for MariaDB version 10\.6 DB instances:
  + The default value for the following parameters has changed from `utf8` to `utf8mb3`: 
    + [character\_set\_client](https://mariadb.com/kb/en/server-system-variables/#character_set_client)
    + [character\_set\_connection](https://mariadb.com/kb/en/server-system-variables/#character_set_connection)
    + [character\_set\_results](https://mariadb.com/kb/en/server-system-variables/#character_set_results)
    + [character\_set\_system](https://mariadb.com/kb/en/server-system-variables/#character_set_system)

    Although the default values have changed for these parameters, there is no functional change\. For more information, see [Supported Character Sets and Collations](https://mariadb.com/kb/en/supported-character-sets-and-collations/)\.
  + The default value of the [ collation\_connection](https://mariadb.com/kb/en/server-system-variables/#collation_connection) parameter has changed from `utf8_general_ci` to `utf8mb3_general_ci`\. Although the default value has changed for this parameter, there is no functional change\.
  + The default value of the [ old\_mode](https://mariadb.com/kb/en/server-system-variables/#old_mode) parameter has changed from unset to `UTF8_IS_UTF8MB3`\. Although the default value has changed for this parameter, there is no functional change\.

For a list of all MariaDB 10\.6 features and their documentation, see [Changes and improvements in MariaDB 10\.6](https://mariadb.com/kb/en/changes-improvements-in-mariadb-106/) and [Release notes \- MariaDB 10\.6 series](https://mariadb.com/kb/en/release-notes-mariadb-106-series/) on the MariaDB website\. 

For a list of unsupported features, see [Features not supported](#MariaDB.Concepts.FeatureNonSupport)\. 

### MariaDB 10\.5 support on Amazon RDS<a name="MariaDB.Concepts.FeatureSupport.10-5"></a>

Amazon RDS supports the following new features for your DB instances running MariaDB version 10\.5 or later: 
+ **InnoDB enhancements** – MariaDB version 10\.5 includes InnoDB enhancements\. For more information, see [ InnoDB: Performance Improvements etc\.](https://mariadb.com/kb/en/changes-improvements-in-mariadb-105/#innodb-performance-improvements-etc)\.
+ **Performance schema updates** – MariaDB version 10\.5 includes performance schema updates\. For more information, see [ Performance Schema Updates to Match MySQL 5\.7 Instrumentation and Tables](https://mariadb.com/kb/en/changes-improvements-in-mariadb-105/#performance-schema-updates-to-match-mysql-57-instrumentation-and-tables)\. 
+ **One file in the InnoDB redo log** – In versions of MariaDB before version 10\.5, the value of the `innodb_log_files_in_group` parameter was set to `2`\. In MariaDB version 10\.5, the value of this parameter is set to `1`\.

  If you are upgrading from a prior version to MariaDB version 10\.5, and you don't modify the parameters, the `innodb_log_file_size` parameter value is unchanged\. However, it applies to one log file instead of two\. The result is that your upgraded MariaDB version 10\.5 DB instance uses half of the redo log size that it was using before the upgrade\. This change can have a noticeable performance impact\. To address this issue, you can double the value of the `innodb_log_file_size` parameter\. For information about modifying parameters, see [Modifying parameters in a DB parameter group](USER_WorkingWithParamGroups.md#USER_WorkingWithParamGroups.Modifying)\. 
+ **SHOW SLAVE STATUS command not supported** – In versions of MariaDB before version 10\.5, the `SHOW SLAVE STATUS` command required the `REPLICATION SLAVE` privilege\. In MariaDB version 10\.5, the equivalent `SHOW REPLICA STATUS` command requires the `REPLICATION REPLICA ADMIN` privilege\. This new privilege isn't granted to the RDS master user\. 

  Instead of using the `SHOW REPLICA STATUS` command, run the new `mysql.rds_replica_status` stored procedure to return similar information\. For more information, see [mysql\.rds\_replica\_status](mysql_rds_replica_status.md)\.
+ **SHOW RELAYLOG EVENTS command not supported** – In versions of MariaDB before version 10\.5, the `SHOW RELAYLOG EVENTS` command required the `REPLICATION SLAVE` privilege\. In MariaDB version 10\.5, this command requires the `REPLICATION REPLICA ADMIN` privilege\. This new privilege isn't granted to the RDS master user\. 
+ **New default values for parameters** – The following parameters have new default values for MariaDB version 10\.5 DB instances:
  + The default value of the [max\_connections](https://mariadb.com/kb/en/server-system-variables/#max_connections) parameter has changed to `LEAST({DBInstanceClassMemory/25165760},12000)`\. For information about the `LEAST` parameter function, see [DB parameter functions](USER_WorkingWithParamGroups.md#USER_ParamFunctions)\. 
  + The default value of the [ innodb\_adaptive\_hash\_index](https://mariadb.com/kb/en/innodb-system-variables/#innodb_adaptive_hash_index) parameter has changed to `OFF` \(`0`\)\.
  + The default value of the [ innodb\_checksum\_algorithm](https://mariadb.com/kb/en/innodb-system-variables/#innodb_checksum_algorithm) parameter has changed to `full_crc32`\.
  + The default value of the [innodb\_log\_file\_size](https://mariadb.com/kb/en/innodb-system-variables/#innodb_log_file_size) parameter has changed to 2 GB\. 

For a list of all MariaDB 10\.5 features and their documentation, see [Changes and improvements in MariaDB 10\.5](https://mariadb.com/kb/en/changes-improvements-in-mariadb-105/) and [Release notes \- MariaDB 10\.5 series](https://mariadb.com/kb/en/release-notes-mariadb-105-series/) on the MariaDB website\. 

For a list of unsupported features, see [Features not supported](#MariaDB.Concepts.FeatureNonSupport)\. 

### MariaDB 10\.4 support on Amazon RDS<a name="MariaDB.Concepts.FeatureSupport.10-4"></a>

Amazon RDS supports the following new features for your DB instances running MariaDB version 10\.4 or later: 
+ **User account security enhancements** – [Password expiration](https://mariadb.com/kb/en/user-password-expiry/) and [account locking](https://mariadb.com/kb/en/account-locking/) improvements
+ **Optimizer enhancements** – [Optimizer trace feature](https://mariadb.com/kb/en/optimizer-trace-overview/)
+ **InnoDB enhancements ** – [Instant DROP COLUMN support](https://mariadb.com/kb/en/alter-table/#drop-column) and instant `VARCHAR` extension for `ROW_FORMAT=DYNAMIC` and `ROW_FORMAT=COMPACT` 
+ **New parameters** – Including [tcp\_nodedelay](https://mariadb.com/kb/en/server-system-variables/#tcp_nodelay), [tls\_version](https://mariadb.com/kb/en/ssltls-system-variables/#tls_version), and [gtid\_cleanup\_batch\_size](https://mariadb.com/kb/en/gtid/#gtid_cleanup_batch_size)

For a list of all MariaDB 10\.4 features and their documentation, see [Changes and improvements in MariaDB 10\.4](https://mariadb.com/kb/en/library/changes-improvements-in-mariadb-104/) and [Release notes \- MariaDB 10\.4 series](https://mariadb.com/kb/en/library/release-notes-mariadb-104-series/) on the MariaDB website\. 

For a list of unsupported features, see [Features not supported](#MariaDB.Concepts.FeatureNonSupport)\. 

### MariaDB 10\.3 support on Amazon RDS<a name="MariaDB.Concepts.FeatureSupport.10-3"></a>

Amazon RDS supports the following new features for your DB instances running MariaDB version 10\.3 or later: 
+ **Oracle compatibility** – PL/SQL compatibility parser, sequences, INTERSECT and EXCEPT to complement UNION, new TYPE OF and ROW TYPE OF declarations, and invisible columns
+ **Temporal data processing** – System versioned tables for querying of past and present states of the database
+ **Flexibility** – User\-defined aggregates, storage\-independent column compression, and proxy protocol support to relay the client IP address to the server
+ **Manageability** – Instant ADD COLUMN operations and fast\-fail data definition language \(DDL\) operations

For a list of all MariaDB 10\.3 features and their documentation, see [Changes & improvements in MariaDB 10\.3](https://mariadb.com/kb/en/library/changes-improvements-in-mariadb-103/) and [Release notes \- MariaDB 10\.3 series](https://mariadb.com/kb/en/library/release-notes-mariadb-103-series/) on the MariaDB website\. 

For a list of unsupported features, see [Features not supported](#MariaDB.Concepts.FeatureNonSupport)\. 

### MariaDB 10\.2 support on Amazon RDS<a name="MariaDB.Concepts.FeatureSupport.10-2"></a>

Amazon RDS supports the following new features for your DB instances running MariaDB version 10\.2 or later: 
+ ALTER USER
+ Common Table Expressions
+ Compressing Events to Reduce Size of the Binary Log
+ CREATE USER — new options for limiting resource usage and TLS/SSL
+ EXECUTE IMMEDIATE
+ Flashback
+ InnoDB — now the default storage engine instead of XtraDB
+ InnoDB — set the buffer pool size dynamically
+ JSON Functions
+ Window Functions
+ WITH

For a list of all MariaDB 10\.2 features and their documentation, see [Changes & improvements in MariaDB 10\.2](https://mariadb.com/kb/en/library/changes-improvements-in-mariadb-102/) and [Release notes \- MariaDB 10\.2 series](https://mariadb.com/kb/en/library/release-notes-mariadb-102-series/) on the MariaDB website\. 

For a list of unsupported features, see [Features not supported](#MariaDB.Concepts.FeatureNonSupport)\. 

## Features not supported<a name="MariaDB.Concepts.FeatureNonSupport"></a>

The following MariaDB features are not supported on Amazon RDS:
+ S3 storage engine
+ Authentication plugin – GSSAPI
+ Authentication plugin – Unix Socket
+ AWS Key Management encryption plugin
+ Delayed replication for MariaDB versions lower than 10\.6
+ Native MariaDB encryption at rest for InnoDB and Aria\.

  You can enable encryption at rest for a MariaDB DB instance by following the instructions in [Encrypting Amazon RDS resources](Overview.Encryption.md)\.
+ HandlerSocket
+ JSON table type for MariaDB versions lower than 10\.6
+ MariaDB ColumnStore
+ MariaDB Galera Cluster
+ Multisource replication
+ MyRocks storage engine for MariaDB versions lower than 10\.6
+ Password validation plugin, `simple_password_check`, and `cracklib_password_check` 
+ Spider storage engine
+ Sphinx storage engine
+ TokuDB storage engine
+ Storage engine\-specific object attributes, as described in [ Engine\-defined new Table/Field/Index attributes](http://mariadb.com/kb/en/mariadb/engine-defined-new-tablefieldindex-attributes/) in the MariaDB documentation
+ Table and tablespace encryption

To deliver a managed service experience, Amazon RDS doesn't provide shell access to DB instances, and it restricts access to certain system procedures and tables that require advanced privileges\. Amazon RDS supports access to databases on a DB instance using any standard SQL client application\. Amazon RDS doesn't allow direct host access to a DB instance by using Telnet, Secure Shell \(SSH\), or Windows Remote Desktop Connection\. 

## Supported storage engines for MariaDB on Amazon RDS<a name="MariaDB.Concepts.Storage"></a>

RDS for MariaDB supports the following storage engines\.

**Topics**
+ [The InnoDB storage engine](#MariaDB.Concepts.Storage.InnoDB)
+ [The MyRocks storage engine](#MariaDB.Concepts.Storage.MyRocks)

Other storage engines aren't currently supported by RDS for MariaDB\.

### The InnoDB storage engine<a name="MariaDB.Concepts.Storage.InnoDB"></a>

Although MariaDB supports multiple storage engines with varying capabilities, not all of them are optimized for recovery and data durability\. InnoDB is the recommended storage engine for MariaDB DB instances on Amazon RDS\. Amazon RDS features such as point\-in\-time restore and snapshot restore require a recoverable storage engine and are supported only for the recommended storage engine for the MariaDB version\.

For more information, see [InnoDB](https://mariadb.com/kb/en/innodb/)\.

### The MyRocks storage engine<a name="MariaDB.Concepts.Storage.MyRocks"></a>

The MyRocks storage engine is available in RDS for MariaDB version 10\.6 and higher\. Before using the MyRocks storage engine in a production database, we recommend that you perform thorough benchmarking and testing to verify any potential benefits over InnoDB for your use case\.

The default parameter group for MariaDB version 10\.6 includes MyRocks parameters\. For more information, see [Parameters for MariaDB](Appendix.MariaDB.Parameters.md) and [Working with DB parameter groups](USER_WorkingWithParamGroups.md)\.

To create a table that uses the MyRocks storage engine, specify `ENGINE=RocksDB` in the `CREATE TABLE` statement\. The following example creates a table that uses the MyRocks storage engine\.

```
CREATE TABLE test (a INT NOT NULL, b CHAR(10)) ENGINE=RocksDB;
```

We strongly recommend that you don't run transactions that span both InnoDB and MyRocks tables\. MariaDB doesn't guarantee ACID \(atomicity, consistency, isolation, durability\) for transactions across storage engines\. Although it is possible to have both InnoDB and MyRocks tables in a DB instance, we don't recommend this approach except during a migration from one storage engine to the other\. When both InnoDB and MyRocks tables exist in a DB instance, each storage engine has its own buffer pool, which might cause performance to degrade\.

MyRocks doesn’t support `SERIALIZABLE` isolation or gap locks\. So, generally you can't use MyRocks with statement\-based replication\. For more information, see [ MyRocks and Replication](https://mariadb.com/kb/en/myrocks-and-replication/)\.

Currently, you can modify only the following MyRocks parameters:
+ [https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_block_cache_size](https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_block_cache_size)
+ [https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_bulk_load](https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_bulk_load)
+ [https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_bulk_load_size](https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_bulk_load_size)
+ [https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_deadlock_detect](https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_deadlock_detect)
+ [https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_deadlock_detect_depth](https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_deadlock_detect_depth)
+ [https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_max_latest_deadlocks](https://mariadb.com/kb/en/myrocks-system-variables/#rocksdb_max_latest_deadlocks)

The MyRocks storage engine and the InnoDB storage engine can compete for memory based on the settings for the `rocksdb_block_cache_size` and `innodb_buffer_pool_size` parameters\. In some cases, you might only intend to use the MyRocks storage engine on a particular DB instance\. If so, we recommend setting the `innodb_buffer_pool_size minimal` parameter to a minimal value and setting the `rocksdb_block_cache_size` as high as possible\.

You can access MyRocks log files by using the [https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBLogFiles.html](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBLogFiles.html) and [https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DownloadDBLogFilePortion.html](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DownloadDBLogFilePortion.html) operations\.

For more information about MyRocks, see [MyRocks](https://mariadb.com/kb/en/myrocks/) on the MariaDB website\.

## MariaDB file size limits in Amazon RDS<a name="RDS_Limits.FileSize.MariaDB"></a>

For MariaDB DB instances, the maximum size of a table is 16 TB when using InnoDB file\-per\-table tablespaces\. This limit also constrains the system tablespace to a maximum size of 16 TB\. InnoDB file\-per\-table tablespaces \(with tables each in their own tablespace\) are set by default for MariaDB DB instances\. This limit isn't related to the maximum storage limit for MariaDB DB instances\. For more information about the storage limit, see [Amazon RDS DB instance storage](CHAP_Storage.md)\.

There are advantages and disadvantages to using InnoDB file\-per\-table tablespaces, depending on your application\. To determine the best approach for your application, see [File\-per\-table tablespaces](https://dev.mysql.com/doc/refman/5.7/en/innodb-file-per-table-tablespaces.html) in the MySQL documentation\.

We don't recommend allowing tables to grow to the maximum file size\. In general, a better practice is to partition data into smaller tables, which can improve performance and recovery times\.

One option that you can use for breaking a large table up into smaller tables is partitioning\. *Partitioning* distributes portions of your large table into separate files based on rules that you specify\. For example, if you store transactions by date, you can create partitioning rules that distribute older transactions into separate files using partitioning\. Then periodically, you can archive the historical transaction data that doesn't need to be readily available to your application\. For more information, see [Partitioning](https://dev.mysql.com/doc/refman/5.7/en/partitioning.html) in the MySQL documentation\.

**To determine the file size of a table**

Use the following SQL command to determine if any of your tables are too large and are candidates for partitioning\. To update table statistics, issue an `ANALYZE TABLE` command on each table\. For more information, see [ANALYZE TABLE statement](https://dev.mysql.com/doc/refman/5.7/en/analyze-table.html) in the MySQL documentation\.

```
1. SELECT TABLE_SCHEMA, TABLE_NAME, 
2.     round(((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024), 2) As "Approximate size (MB)", DATA_FREE 
3.     FROM information_schema.TABLES
4.     WHERE TABLE_SCHEMA NOT IN ('mysql', 'information_schema', 'performance_schema');
```

**To enable InnoDB file\-per\-table tablespaces**
+ To enable InnoDB file\-per\-table tablespaces, set the `innodb_file_per_table` parameter to `1` in the parameter group for the DB instance\.

**To disable InnoDB file\-per\-table tablespaces**
+ To disable InnoDB file\-per\-table tablespaces, set the `innodb_file_per_table` parameter to `0` in the parameter group for the DB instance\.

For information on updating a parameter group, see [Working with DB parameter groups](USER_WorkingWithParamGroups.md)\.

When you have enabled or disabled InnoDB file\-per\-table tablespaces, you can issue an `ALTER TABLE` command\. You can use this command to move a table from the global tablespace to its own tablespace\. Or you can move a table from its own tablespace to the global tablespace\. Following is an example\.

```
1. ALTER TABLE table_name ENGINE=InnoDB, ALGORITHM=COPY; 
```

## MariaDB security on Amazon RDS<a name="MariaDB.Concepts.UsersAndPrivileges"></a>

Security for MariaDB DB instances is managed at three levels:
+ AWS Identity and Access Management controls who can perform Amazon RDS management actions on DB instances\. When you connect to AWS using IAM credentials, your IAM account must have IAM policies that grant the permissions required to perform Amazon RDS management operations\. For more information, see [Identity and access management in Amazon RDS](UsingWithRDS.IAM.md)\.
+ When you create a DB instance, you use either a VPC security group or a DB security group to control which devices and Amazon EC2 instances can open connections to the endpoint and port of the DB instance\. These connections can be made using Secure Socket Layer \(SSL\)\. In addition, firewall rules at your company can control whether devices running at your company can open connections to the DB instance\.
+ Once a connection has been opened to a MariaDB DB instance, authentication of the login and permissions are applied the same way as in a stand\-alone instance of MariaDB\. Commands such as `CREATE USER`, `RENAME USER`, `GRANT`, `REVOKE`, and `SET PASSWORD` work just as they do in stand\-alone databases, as does directly modifying database schema tables\.

 When you create an Amazon RDS DB instance, the master user has the following default privileges: 
+  `alter` 
+  `alter routine` 
+  `create` 
+  `create routine` 
+  `create temporary tables` 
+  `create user` 
+  `create view` 
+  `delete` 
+  `drop` 
+  `event` 
+  `execute` 
+  `grant option` 
+  `index` 
+  `insert` 
+  `lock tables` 
+  `process` 
+  `references` 
+  `reload` 

  This privilege is limited on MariaDB DB instances\. It doesn't grant access to the FLUSH LOGS or FLUSH TABLES WITH READ LOCK operations\.
+  `replication client` 
+  `replication slave` 
+  `select` 
+  `show databases` 
+  `show view` 
+  `trigger` 
+  `update` 

For more information about these privileges, see [User account management](http://mariadb.com/kb/en/mariadb/grant/) in the MariaDB documentation\.

**Note**  
Although you can delete the master user on a DB instance, we don't recommend doing so\. To recreate the master user, use the `ModifyDBInstance` API or the `modify-db-instance` AWS CLI and specify a new master user password with the appropriate parameter\. If the master user does not exist in the instance, the master user is created with the specified password\. 

To provide management services for each DB instance, the `rdsadmin` user is created when the DB instance is created\. Attempting to drop, rename, change the password for, or change privileges for the `rdsadmin` account results in an error\.

To allow management of the DB instance, the standard `kill` and `kill_query` commands have been restricted\. The Amazon RDS commands `mysql.rds_kill`, `mysql.rds_kill_query`, and `mysql.rds_kill_query_id` are provided for use in MariaDB and also MySQL so that you can end user sessions or queries on DB instances\. 

## Using SSL with a MariaDB DB instance<a name="MariaDB.Concepts.SSLSupport"></a>

Amazon RDS supports Secure Sockets Layer \(SSL\) connections with DB instances running the MariaDB database engine\. MariaDB uses OpenSSL for secure connections\.

Amazon RDS creates an SSL certificate and installs the certificate on the DB instance when Amazon RDS provisions the instance\. These certificates are signed by a certificate authority\. The SSL certificate includes the DB instance endpoint as the Common Name \(CN\) for the SSL certificate to guard against spoofing attacks\. 

For information about downloading certificates, see [Using SSL/TLS to encrypt a connection to a DB instance](UsingWithRDS.SSL.md)\.

Amazon RDS for MariaDB supports Transport Layer Security \(TLS\) versions 1\.0, 1\.1, 1\.2, and 1\.3\. The following table shows the TLS support for MySQL versions\. 


****  

| MariaDB version | TLS 1\.0 | TLS 1\.1 | TLS 1\.2 | TLS 1\.3 | 
| --- | --- | --- | --- | --- | 
|  MariaDB 10\.6  |  Supported  |  Supported  |  Supported  |  Supported  | 
|  MariaDB 10\.5  |  Supported  |  Supported  |  Supported  |  Supported  | 
|  MariaDB 10\.4  |  Supported  |  Supported  |  Supported  |  Supported  | 
|  MariaDB 10\.3  |  Supported  |  Supported  |  Supported  |  Supported  | 
|  MariaDB 10\.2  |  Supported  |  Supported  |  Supported  |  Supported  | 

**Important**  
The `mysql` client program parameters are slightly different if you are using the MySQL 5\.7 version, the MySQL 8\.0 version, or the MariaDB version\.  
To find out which version you have, run the `mysql` command with the `--version` option\. In the following example, the output shows that the client program is from MariaDB\.  

```
$ mysql --version
mysql  Ver 15.1 Distrib 10.5.9-MariaDB, for osx10.15 (x86_64) using readline 5.1
```
Most Linux distributions, such as Amazon Linux, CentOS, SUSE, and Debian have replaced MySQL with MariaDB, and the `mysql` version in them is from MariaDB\.

To encrypt connections using the default mysql client, launch the mysql client using the `--ssl-ca` parameter to reference the public key, as shown in the examples following\.

The following example shows how to launch the client using the `--ssl-ca` parameter using the MySQL 5\.7 client or later:

```
mysql -h myinstance.123456789012.rds-us-east-1.amazonaws.com
--ssl-ca=[full path]global-bundle.pem --ssl-mode=REQUIRED
```

The following example shows how to launch the client using the `--ssl-ca` parameter using the MariaDB client:

```
mysql -h myinstance.123456789012.rds-us-east-1.amazonaws.com
--ssl-ca=[full path]global-bundle.pem --ssl
```

For information about downloading certificate bundles, see [Using SSL/TLS to encrypt a connection to a DB instance](UsingWithRDS.SSL.md)\.

You can require SSL connections for specific users accounts\. For example, you can use one of the following statements, depending on your MariaDB version, to require SSL connections on the user account `encrypted_user`\.

Use the following statement\.

```
ALTER USER 'encrypted_user'@'%' REQUIRE SSL;            
```

For more information on SSL connections with MariaDB, see [SSL overview](http://mariadb.com/kb/en/mariadb/ssl-connections/) in the MariaDB documentation\. 

## Cache warming<a name="MariaDB.Concepts.XtraDBCacheWarming"></a>

InnoDB cache warming can provide performance gains for your MariaDB DB instance by saving the current state of the buffer pool when the DB instance is shut down, and then reloading the buffer pool from the saved information when the DB instance starts up\. This approach bypasses the need for the buffer pool to "warm up" from normal database use and instead preloads the buffer pool with the pages for known common queries\. For more information on cache warming, see [ Dumping and restoring the buffer pool](http://mariadb.com/kb/en/mariadb/xtradbinnodb-buffer-pool/#dumping-and-restoring-the-buffer-pool) in the MariaDB documentation\.

Cache warming is enabled by default on MariaDB 10\.2 and higher DB instances\. To enable it, set the `innodb_buffer_pool_dump_at_shutdown` and `innodb_buffer_pool_load_at_startup` parameters to 1 in the parameter group for your DB instance\. Changing these parameter values in a parameter group affects all MariaDB DB instances that use that parameter group\. To enable cache warming for specific MariaDB DB instances, you might need to create a new parameter group for those DB instances\. For information on parameter groups, see [Working with DB parameter groups](USER_WorkingWithParamGroups.md)\.

Cache warming primarily provides a performance benefit for DB instances that use standard storage\. If you use PIOPS storage, you don't commonly see a significant performance benefit\.

**Important**  
If your MariaDB DB instance doesn't shut down normally, such as during a failover, then the buffer pool state isn't saved to disk\. In this case, MariaDB loads whatever buffer pool file is available when the DB instance is restarted\. No harm is done, but the restored buffer pool might not reflect the most recent state of the buffer pool before the restart\. To ensure that you have a recent state of the buffer pool available to warm the cache on startup, we recommend that you periodically dump the buffer pool "on demand\." You can dump or load the buffer pool on demand\.  
You can create an event to dump the buffer pool automatically and at a regular interval\. For example, the following statement creates an event named `periodic_buffer_pool_dump` that dumps the buffer pool every hour\.   

```
1. CREATE EVENT periodic_buffer_pool_dump 
2.    ON SCHEDULE EVERY 1 HOUR 
3.    DO CALL mysql.rds_innodb_buffer_pool_dump_now();
```
For more information, see [Events](http://mariadb.com/kb/en/mariadb/stored-programs-and-views-events/) in the MariaDB documentation\.

### Dumping and loading the buffer pool on demand<a name="MariaDB.Concepts.XtraDBCacheWarming.OnDemand"></a>

You can save and load the cache on demand using the following stored procedures:
+ To dump the current state of the buffer pool to disk, call the [mysql\.rds\_innodb\_buffer\_pool\_dump\_now](mysql_rds_innodb_buffer_pool_dump_now.md) stored procedure\.
+ To load the saved state of the buffer pool from disk, call the [mysql\.rds\_innodb\_buffer\_pool\_load\_now](mysql_rds_innodb_buffer_pool_load_now.md) stored procedure\.
+ To cancel a load operation in progress, call the [mysql\.rds\_innodb\_buffer\_pool\_load\_abort](mysql_rds_innodb_buffer_pool_load_abort.md) stored procedure\.

## Database parameters for MariaDB<a name="MariaDB.Concepts.Parameters"></a>

By default, a MariaDB DB instance uses a DB parameter group that is specific to a MariaDB database\. This parameter group contains some but not all of the parameters contained in the Amazon RDS DB parameter groups for the MySQL database engine\. It also contains a number of new, MariaDB\-specific parameters\. For more information on the parameters available for the RDS for MariaDB DB engine, see [Parameters for MariaDB](Appendix.MariaDB.Parameters.md)\.

## Common DBA tasks for MariaDB<a name="MariaDB.Concepts.DBA.Tasks"></a>

Ending sessions or queries, skipping replication errors, working with InnoDB tablespaces to improve crash recovery times, and managing the global status history are common DBA tasks you might perform in a MariaDB DB instance\. You can handle these tasks just as in a MySQL DB instance, as described in [Common DBA tasks for MySQL DB instances](Appendix.MySQL.CommonDBATasks.md)\. The crash recovery instructions there refer to the MySQL InnoDB engine, but they are applicable to a MariaDB DB instance running InnoDB as well\.

## Local time zone for MariaDB DB instances<a name="MariaDB.Concepts.LocalTimeZone"></a>

By default, the time zone for a MariaDB DB instance is Universal Time Coordinated \(UTC\)\. You can set the time zone for your DB instance to the local time zone for your application instead\.

To set the local time zone for a DB instance, set the `time_zone` parameter in the parameter group for your DB instance to one of the supported values listed later in this section\. When you set the `time_zone` parameter for a parameter group, all DB instances and read replicas that are using that parameter group change to use the new local time zone\. For information on setting parameters in a parameter group, see [Working with DB parameter groups](USER_WorkingWithParamGroups.md)\.

After you set the local time zone, all new connections to the database reflect the change\. If you have any open connections to your database when you change the local time zone, you won't see the local time zone update until after you close the connection and open a new connection\.

You can set a different local time zone for a DB instance and one or more of its read replicas\. To do this, use a different parameter group for the DB instance and the replica or replicas and set the `time_zone` parameter in each parameter group to a different local time zone\.

If you are replicating across AWS Regions, then the source DB instance and the read replica use different parameter groups \(parameter groups are unique to an AWS Region\)\. To use the same local time zone for each instance, you must set the `time_zone` parameter in the instance's and read replica's parameter groups\.

When you restore a DB instance from a DB snapshot, the local time zone is set to UTC\. You can update the time zone to your local time zone after the restore is complete\. If you restore a DB instance to a point in time, then the local time zone for the restored DB instance is the time zone setting from the parameter group of the restored DB instance\.

You can set your local time zone to one of the following values\.


****  

|  |  | 
| --- |--- |
| `Africa/Cairo` | `Asia/Riyadh` | 
| `Africa/Casablanca` | `Asia/Seoul` | 
| `Africa/Harare` | `Asia/Shanghai` | 
| `Africa/Monrovia` | `Asia/Singapore` | 
| `Africa/Nairobi` | `Asia/Taipei` | 
| `Africa/Tripoli` | `Asia/Tehran` | 
| `Africa/Windhoek` | `Asia/Tokyo` | 
| `America/Araguaina` | `Asia/Ulaanbaatar` | 
| `America/Asuncion` | `Asia/Vladivostok` | 
| `America/Bogota` | `Asia/Yakutsk` | 
| `America/Buenos_Aires` | `Asia/Yerevan` | 
| `America/Caracas` | `Atlantic/Azores` | 
| `America/Chihuahua` | `Australia/Adelaide` | 
| `America/Cuiaba` | `Australia/Brisbane` | 
| `America/Denver` | `Australia/Darwin` | 
| `America/Fortaleza` | `Australia/Hobart` | 
| `America/Guatemala` | `Australia/Perth` | 
| `America/Halifax` | `Australia/Sydney` | 
| `America/Manaus` | `Brazil/East` | 
| `America/Matamoros` | `Canada/Newfoundland` | 
| `America/Monterrey` | `Canada/Saskatchewan` | 
| `America/Montevideo` | `Canada/Yukon` | 
| `America/Phoenix` | `Europe/Amsterdam` | 
| `America/Santiago` | `Europe/Athens` | 
| `America/Tijuana` | `Europe/Dublin` | 
| `Asia/Amman` | `Europe/Helsinki` | 
| `Asia/Ashgabat` | `Europe/Istanbul` | 
| `Asia/Baghdad` | `Europe/Kaliningrad` | 
| `Asia/Baku` | `Europe/Moscow` | 
| `Asia/Bangkok` | `Europe/Paris` | 
| `Asia/Beirut` | `Europe/Prague` | 
| `Asia/Calcutta` | `Europe/Sarajevo` | 
| `Asia/Damascus` | `Pacific/Auckland` | 
| `Asia/Dhaka` | `Pacific/Fiji` | 
| `Asia/Irkutsk` | `Pacific/Guam` | 
| `Asia/Jerusalem` | `Pacific/Honolulu` | 
| `Asia/Kabul` | `Pacific/Samoa` | 
| `Asia/Karachi` | `US/Alaska` | 
| `Asia/Kathmandu` | `US/Central` | 
| `Asia/Krasnoyarsk` | `US/Eastern` | 
| `Asia/Magadan` | `US/East-Indiana` | 
| `Asia/Muscat` | `US/Pacific` | 
| `Asia/Novosibirsk` | `UTC` | 

## InnoDB reserved word<a name="MariaDB.Concepts.InnodbDatabaseName"></a>

`InnoDB` is a reserved word for RDS for MariaDB\. You can't use this name for a MariaDB database\.

## Deprecated versions for Amazon RDS for MariaDB<a name="MariaDB.Concepts.DeprecatedVersions"></a>

Amazon RDS for MariaDB version 10\.0 and 10\.1 are deprecated\.

For more information, see [ Announcement: Extending end\-of\-life Process for Amazon RDS for MariaDB 10\.0 and 10\.1](http://forums.aws.amazon.com/ann.jspa?annID=8571)\.

For information about the Amazon RDS deprecation policy for MariaDB, see [Amazon RDS FAQs](http://aws.amazon.com/rds/faqs/)\.
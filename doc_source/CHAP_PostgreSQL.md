# PostgreSQL on Amazon RDS<a name="CHAP_PostgreSQL"></a>

Amazon RDS supports DB instances running several versions of PostgreSQL\. For a list of supported versions, see [Supported PostgreSQL database versions](#PostgreSQL.Concepts.General.DBVersions)\.

**Note**  
Deprecation of PostgreSQL 9\.6 is scheduled for April 26, 2022\. For more information, see [Deprecation of PostgreSQL version 9\.6](#PostgreSQL.Concepts.General.DBVersions.Deprecation96)\. 

You can create DB instances and DB snapshots, point\-in\-time restores and backups\. DB instances running PostgreSQL support Multi\-AZ deployments, read replicas, Provisioned IOPS, and can be created inside a VPC\. You can also use Secure Socket Layer \(SSL\) to connect to a DB instance running PostgreSQL\.

Before creating a DB instance, you should complete the steps in the [Setting up for Amazon RDS](CHAP_SettingUp.md) section of this guide\.

You can use any standard SQL client application to run commands for the instance from your client computer\. Such applications include *pgAdmin*, a popular Open Source administration and development tool for PostgreSQL, or *psql*, a command line utility that is part of a PostgreSQL installation\. To deliver a managed service experience, Amazon RDS doesn't provide host access to DB instances, and it restricts access to certain system procedures and tables that require advanced privileges\. Amazon RDS supports access to databases on a DB instance using any standard SQL client application\. Amazon RDS doesn't allow direct host access to a DB instance by using Telnet or Secure Shell \(SSH\)\.

Amazon RDS for PostgreSQL is compliant with many industry standards\. For example, you can use Amazon RDS for PostgreSQL databases to build HIPAA\-compliant applications and to store healthcare\-related information, including protected health information \(PHI\) under a completed Business Associate Agreement \(BAA\) with AWS\. Amazon RDS for PostgreSQL also meets Federal Risk and Authorization Management Program \(FedRAMP\) security requirements\. Amazon RDS for PostgreSQL has received a FedRAMP Joint Authorization Board \(JAB\) Provisional Authority to Operate \(P\-ATO\) at the FedRAMP HIGH Baseline within the AWS GovCloud \(US\) Regions\. For more information on supported compliance standards, see [AWS cloud compliance](http://aws.amazon.com/compliance/)\.

To import PostgreSQL data into a DB instance, follow the information in the [Importing data into PostgreSQL on Amazon RDS](PostgreSQL.Procedural.Importing.md) section\.

**Topics**
+ [Common management tasks for RDS for PostgreSQL](#CHAP_PostgreSQL.CommonTasks)
+ [Working with the database preview environment](#working-with-the-database-preview-environment)
+ [Limitations for PostgreSQL DB instances](#PostgreSQL.Concepts.General.Limits)
+ [Supported PostgreSQL database versions](#PostgreSQL.Concepts.General.DBVersions)
+ [Deprecated versions for Amazon RDS for PostgreSQL](#PostgreSQL.Concepts.General.DeprecatedVersions)
+ [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)
+ [PostgreSQL features supported by RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport)
+ [Connecting to a DB instance running the PostgreSQL database engine](USER_ConnectToPostgreSQLInstance.md)
+ [Security with RDS for PostgreSQL](PostgreSQL.Concepts.General.Security.md)
+ [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)
+ [Upgrading a PostgreSQL DB snapshot engine version](USER_UpgradeDBSnapshot.PostgreSQL.md)
+ [Working with PostgreSQL read replicas in Amazon RDS](USER_PostgreSQL.Replication.ReadReplicas.md)
+ [Importing data into PostgreSQL on Amazon RDS](PostgreSQL.Procedural.Importing.md)
+ [Exporting data from an RDS for PostgreSQL DB instance to Amazon S3](postgresql-s3-export.md)
+ [Common DBA tasks for PostgreSQL](Appendix.PostgreSQL.CommonDBATasks.md)

## Common management tasks for RDS for PostgreSQL<a name="CHAP_PostgreSQL.CommonTasks"></a>

The following are the common management tasks you perform with an Amazon RDS for PostgreSQL DB instance, with links to relevant documentation for each task\.


| Task area | Relevant documentation | 
| --- | --- | 
|  **Setting up Amazon RDS for first\-time use** There are prerequisites you must complete before you create your DB instance\. For example, DB instances are created by default with a firewall that prevents access to it\. You therefore must create a security group with the correct IP addresses and network configuration to access the DB instance\.   |  [Setting up for Amazon RDS](CHAP_SettingUp.md)  | 
|  **Understanding Amazon RDS DB instances** If you are creating a DB instance for production purposes, you should understand how instance classes, storage types, and Provisioned IOPS work in Amazon RDS\.   |  [DB instance classes](Concepts.DBInstanceClass.md) [Amazon RDS storage types](CHAP_Storage.md#Concepts.Storage) [Provisioned IOPS SSD storage](CHAP_Storage.md#USER_PIOPS)  | 
|  **Finding supported PostgreSQL versions** Amazon RDS supports several versions of PostgreSQL\.   |  [Supported PostgreSQL database versions](#PostgreSQL.Concepts.General.DBVersions)  | 
|  **Setting up high availability and failover support** A production DB instance should use Multi\-AZ deployments\. Multi\-AZ deployments provide increased availability, data durability, and fault tolerance for DB instances\.   |  [Multi\-AZ deployments for high availability](Concepts.MultiAZ.md)  | 
|  **Understanding the Amazon Virtual Private Cloud \(VPC\) network** If your AWS account has a default VPC, then your DB instance is automatically created inside the default VPC\. In some cases, your account might not have a default VPC, and you might want the DB instance in a VPC\. In these cases, create the VPC and subnet groups before you create the DB instance\.   |  [Determining whether you are using the EC2\-VPC or EC2\-Classic platform](USER_VPC.FindDefaultVPC.md) [Working with a DB instance in a VPC](USER_VPC.WorkingWithRDSInstanceinaVPC.md)  | 
|  **Importing data into Amazon RDS PostgreSQL** You can use several different tools to import data into your PostgreSQL DB instance on Amazon RDS\.   |  [Importing data into PostgreSQL on Amazon RDS](PostgreSQL.Procedural.Importing.md)  | 
|  **Setting up read\-only read replicas \(primary and standbys\)** RDS for PostgreSQL supports read replicas in both the same AWS Region and in a different AWS Region from the primary instance\.  |  [Working with read replicas](USER_ReadRepl.md) [Working with PostgreSQL read replicas in Amazon RDS](USER_PostgreSQL.Replication.ReadReplicas.md) [Creating a read replica in a different AWS Region](USER_ReadRepl.XRgn.md)  | 
|  **Understanding security groups** By default, DB instances are created with a firewall that prevents access to them\. You therefore must create a security group with the correct IP addresses and network configuration to access the DB instance\.  In general, if your DB instance is on the EC2\-Classic platform, you need to create a DB security group\. If your DB instance is on the EC2\-VPC platform, you need to create a VPC security group\.   |  [Determining whether you are using the EC2\-VPC or EC2\-Classic platform](USER_VPC.FindDefaultVPC.md) [Controlling access with security groups](Overview.RDSSecurityGroups.md)  | 
|  **Setting up parameter groups and features** If your DB instance is going to require specific database parameters, you should create a parameter group before you create the DB instance\.   |  [Working with DB parameter groups](USER_WorkingWithParamGroups.md)  | 
|  **Performing common DBA tasks for PostgreSQL** Some of the more common tasks for PostgreSQL DBAs include:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html)  |  [Common DBA tasks for PostgreSQL](Appendix.PostgreSQL.CommonDBATasks.md)  | 
|  **Connecting to your PostgreSQL DB instance** After creating a security group and associating it to a DB instance, you can connect to the DB instance using any standard SQL client application such as `psql` or `pgAdmin`\.  |  [Connecting to a DB instance running the PostgreSQL database engine](USER_ConnectToPostgreSQLInstance.md) [Using SSL with a PostgreSQL DB instance](PostgreSQL.Concepts.General.SSL.md)  | 
|  **Backing up and restoring your DB instance** You can configure your DB instance to take automated backups, or take manual snapshots, and then restore instances from the backups or snapshots\.   |  [Backing up and restoring an Amazon RDS DB instance](CHAP_CommonTasks.BackupRestore.md)  | 
|  **Monitoring the activity and performance of your DB instance** You can monitor a PostgreSQL DB instance by using CloudWatch Amazon RDS metrics, events, and enhanced monitoring\.   |  [Viewing metrics in the Amazon RDS console](USER_Monitoring.md) [Viewing Amazon RDS events](USER_ListEvents.md)  | 
|  **Upgrading the PostgreSQL database version** You can do both major and minor version upgrades for your PostgreSQL DB instance\.   |  [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md) [ Choosing a major version upgrade for PostgreSQL ](USER_UpgradeDBInstance.PostgreSQL.md#USER_UpgradeDBInstance.PostgreSQL.MajorVersion)  | 
|  **Working with log files** You can access the log files for your PostgreSQL DB instance\.   |  [PostgreSQL database log files](USER_LogAccess.Concepts.PostgreSQL.md)  | 
|  **Understanding the best practices for PostgreSQL DB instances** Find some of the best practices for working with PostgreSQL on Amazon RDS\.   |  [Best practices for working with PostgreSQL](CHAP_BestPractices.md#CHAP_BestPractices.PostgreSQL)  | 

## Working with the database preview environment<a name="working-with-the-database-preview-environment"></a>

When you create a DB instance in Amazon RDS, you know that the PostgreSQL version it's based on has been tested and is fully supported by Amazon\. The PostgreSQL community releases new versions and new extensions continuously\. You can try out new PostgreSQL versions and extensions before they are fully supported\. To do that, you can create a new DB instance in the Database Preview Environment\. 

DB instances in the Database Preview Environment are similar to DB instances in a production environment\. However, keep in mind several important factors:
+ All DB instances are deleted 60 days after you create them, along with any backups and snapshots\.
+ You can only create a DB instance in a virtual private cloud \(VPC\) based on the Amazon VPC service\.
+ You can only create M6g, M5, T3, R6g, and R5 instance types\. For more information about RDS instance classes, see [DB instance classes](Concepts.DBInstanceClass.md)\. 
+ You can only use General Purpose SSD and Provisioned IOPS SSD storage\. 
+ You can't get help from AWS Support with DB instances\. You can post your questions in the [ RDS database preview environment forum](https://forums.aws.amazon.com/forum.jspa?forumID=301)\.
+ You can't copy a snapshot of a DB instance to a production environment\.
+ You can use both single\-AZ and multi\-AZ deployments\.
+ You can use standard PostgreSQL dump and load functions to export databases from or import databases to the Database Preview Environment\.

**Topics**
+ [Features not supported in the preview environment](#preview-environment-exclusions)
+ [Creating a new DB instance in the preview environment](#create-db-instance-in-preview-environment)

### Features not supported in the preview environment<a name="preview-environment-exclusions"></a>

The following features are not available in the preview environment:
+ Cross\-region snapshot copy
+ Cross\-region read replicas

### Creating a new DB instance in the preview environment<a name="create-db-instance-in-preview-environment"></a>

Use the following procedure to create a DB instance in the preview environment\.

**To create a DB instance in the preview environment**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1.  Choose **Dashboard** from the navigation pane\. 

1. Choose **Switch to database preview environment**\.   
![\[Dialog box to select the preview environment\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/instance_preview.png)

   You also can navigate directly to the [Database preview environment](https://us-east-2.console.aws.amazon.com/rds-preview/home?region=us-east-2#)\.
**Note**  
If you want to create an instance in the Database Preview Environment with the API or CLI, the endpoint is `rds-preview.us-east-2.amazonaws.com`\.

1. Continue with the procedure as described in [Console](USER_CreateDBInstance.md#USER_CreateDBInstance.CON)\.

## Limitations for PostgreSQL DB instances<a name="PostgreSQL.Concepts.General.Limits"></a>

The following is a list of limitations for RDS for PostgreSQL:
+ You can have up to 40 PostgreSQL DB instances\.
+ For storage limits, see [Amazon RDS DB instance storage](CHAP_Storage.md)\.
+ Amazon RDS reserves up to 3 connections for system maintenance\. If you specify a value for the user connections parameter, you need to add 3 to the number of connections that you expect to use\. 

## Supported PostgreSQL database versions<a name="PostgreSQL.Concepts.General.DBVersions"></a>

Amazon RDS supports DB instances running several editions of PostgreSQL\. You can specify any currently supported PostgreSQL version when creating a new DB instance\. You can specify the major version \(such as PostgreSQL 10\), and any supported minor version for the specified major version\. If no version is specified, Amazon RDS defaults to a supported version, typically the most recent version\. If a major version is specified but a minor version is not, Amazon RDS defaults to a recent release of the major version you have specified\. 

To see a list of supported versions, as well as defaults for newly created DB instances, use the [https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-engine-versions.html](https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-engine-versions.html) AWS CLI command\. For example, to display the default PostgreSQL engine version, use the following command:

```
aws rds describe-db-engine-versions ––default-only ––engine postgres
```

**Topics**
+ [Deprecation of PostgreSQL version 9\.6](#PostgreSQL.Concepts.General.DBVersions.Deprecation96)
+ [PostgreSQL 14 versions](#PostgreSQL.Concepts.General.version14)
+ [PostgreSQL 13 versions](#PostgreSQL.Concepts.General.version13)
+ [PostgreSQL 12 versions](#PostgreSQL.Concepts.General.version12)
+ [PostgreSQL 11 versions](#PostgreSQL.Concepts.General.version11)
+ [PostgreSQL 10 versions](#PostgreSQL.Concepts.General.version10)
+ [PostgreSQL 9\.6 versions](#PostgreSQL.Concepts.General.version96)

### Deprecation of PostgreSQL version 9\.6<a name="PostgreSQL.Concepts.General.DBVersions.Deprecation96"></a>

On March 31, 2022, Amazon RDS plans to deprecate support for PostgreSQL 9\.6 using the following schedule\. This extends the previously announced date of January 18, 2022 to April 26, 2022\. You should upgrade all your PostgreSQL 9\.6 DB instances to PostgreSQL 12 or higher as soon as possible\. We recommend that you first upgrade to minor version 9\.6\.20 or higher and then upgrade directly to PostgreSQL 12 rather than upgrading to an intermediate major version\. For more information, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 


| Action or recommendation | Dates | 
| --- | --- | 
|  The PostgreSQL community discontinued support for PostgreSQL 9\.6, and will no longer provide bug fixes or security patches for this version\.   |  November 11, 2021  | 
|  Start upgrading RDS for PostgreSQL 9\.6 DB instances to PostgreSQL 12 or higher as soon as possible\. Although you can continue to restore PostgreSQL 9\.6 snapshots and create read replicas with version 9\.6, be aware of the other critical dates in this deprecation schedule and their impact\.   |  Now – March 31, 2022  | 
|  After this date, you can't create new Amazon RDS instances with PostgreSQL major version 9\.6 from either the AWS Management Console or the AWS CLI\.   |  March 31, 2022  | 
|  Amazon RDS automatically upgrades PostgreSQL 9\.6 instances to version 12\. If you restore a PostgreSQL 9\.6 database snapshot, Amazon RDS automatically upgrades the restored database to PostgreSQL 12\.   |  April 26, 2022  | 

For more information about RDS for PostgreSQL 9\.6 deprecation, see [ Announcement: Extending end\-of\-life process for Amazon RDS for PostgreSQL 9\.6](http://forums.aws.amazon.com/ann.jspa?annID=9092)\.

### PostgreSQL 14 versions<a name="PostgreSQL.Concepts.General.version14"></a>

**Topics**
+ [PostgreSQL version 14\.1 on Amazon RDS](#PostgreSQL.Concepts.General.version141)

#### PostgreSQL version 14\.1 on Amazon RDS<a name="PostgreSQL.Concepts.General.version141"></a>

PostgreSQL version 14\.1 is now available on Amazon RDS\. PostgreSQL contains several improvements that were announced in [PostgreSQL 14](https://www.postgresql.org/docs/14/release-14.html)\.

This version also includes the following changes:
+ The [old\_snapshot ](https://www.postgresql.org/docs/14/oldsnapshot.html) extension 1\.0 is added\. If you set `old_snapshot_threshold` to a value, this extension lets you map transaction ID to a timestamp\. 
+ The [amcheck](https://www.postgresql.org/docs/14/amcheck.html) extension is updated to version 1\.3\.
+ The [btree\_gist](http://www.postgresql.org/docs/14/btree-gist.html) extension is updated to version 1\.6\.
+ The [cube](http://www.postgresql.org/docs/14/cube.html) extension is updated to version 1\.5\.
+ The [hstore](http://www.postgresql.org/docs/14/hstore.html) extension is updated to version 1\.8\.
+ The [intarray](http://www.postgresql.org/docs/14/intarray.html) extension is updated to version 1\.5\.
+ The [pageinspect](https://www.postgresql.org/docs/current/pageinspect.html) extension is updated to version 1\.9\.
+ The [pg\_cron]() extension is upgraded to version 1\.4
+ The [pg\_partman]() extension is upgrade to version 4\.6\.0\.
+ The [pg\_repack](http://reorg.github.io/pg_repack/) extension is updated to version 1\.4\.7\.
+ The [pg\_stat\_statements](http://www.postgresql.org/docs/14/pgstatstatements.html) extension is updated to version 1\.9\.
+ The [pg\_trgm](http://www.postgresql.org/docs/14/pgtrgm.html) extension is updated to version 1\.6\.
+ The [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) extension is updated to version 1\.6\.
+ The [pgrouting](http://docs.pgrouting.org/latest/en/index.html) extension is updated to version 3\.2\.0\.
+ The [postgres\_fdw](http://www.postgresql.org/docs/14/postgres-fdw.html) extension is updated to version 1\.1\.

For information on all extensions, see [PostgreSQL version 14 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.14x)\.

### PostgreSQL 13 versions<a name="PostgreSQL.Concepts.General.version13"></a>

**Topics**
+ [PostgreSQL version 13\.5 on Amazon RDS](#PostgreSQL.Concepts.General.version135)
+ [PostgreSQL version 13\.4 on Amazon RDS](#PostgreSQL.Concepts.General.version134)
+ [PostgreSQL version 13\.3 on Amazon RDS](#PostgreSQL.Concepts.General.version133)
+ [PostgreSQL version 13\.2 on Amazon RDS](#PostgreSQL.Concepts.General.version132)
+ [PostgreSQL version 13\.1 on Amazon RDS](#PostgreSQL.Concepts.General.version131)

#### PostgreSQL version 13\.5 on Amazon RDS<a name="PostgreSQL.Concepts.General.version135"></a>

PostgreSQL version 13\.5 is now available on Amazon RDS\. PostgreSQL contains several improvements that were announced in [PostgreSQL 13\.5](https://www.postgresql.org/docs/release/13.5/)\.

This version also includes the following change:
+  The [pg\_cron](https://github.com/citusdata/pg_cron) extension is updated to 1\.4\.1

For information on all extensions, see [PostgreSQL version 13 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x)\.

#### PostgreSQL version 13\.4 on Amazon RDS<a name="PostgreSQL.Concepts.General.version134"></a>

PostgreSQL version 13\.4 is now available on Amazon RDS\. PostgreSQL contains several improvements that were announced in [PostgreSQL 13\.4](https://www.postgresql.org/docs/release/13.4/)\.

This version also includes the following changes:
+ The [spi module](https://www.postgresql.org/docs/13/contrib-spi.html) extensions refint, autoinc, inset\_username, and moddatetime version 1\.0 are added\. 
+ The [pgrouting](http://docs.pgrouting.org/latest/en/index.html) extension is updated to version 3\.1\.3\.
+ The `pglogical` extension is updated to version 2\.4\.0\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.1\.4, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_raster](https://postgis.net/docs/raster.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 13 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x)\.

#### PostgreSQL version 13\.3 on Amazon RDS<a name="PostgreSQL.Concepts.General.version133"></a>

PostgreSQL version 13\.3 is now available on Amazon RDS\. PostgreSQL contains several improvements that were announced in [PostgreSQL 13\.3](https://www.postgresql.org/docs/release/13.3/)\.

This version also includes the following changes:
+ The [oracle\_fdw](https://github.com/laurenz/oracle_fdw) extension version 2\.3\.0 is added\. For more information, see [Accessing external data with the oracle\_fdw extension](Appendix.PostgreSQL.CommonDBATasks.md#postgresql-oracle-fdw)\.
+ The [orafce](https://github.com/orafce/orafce) extension is updated to version 3\.15\.
+ The [pg\_cron](PostgreSQL_pg_cron.md) extension is updated to version 1\.3\.1\.
+ The [pg\_partman](PostgreSQL_Partitions.md) extension is updated to version 4\.5\.1\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.0\.3, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_raster](https://postgis.net/docs/raster.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 13 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x)\.

#### PostgreSQL version 13\.2 on Amazon RDS<a name="PostgreSQL.Concepts.General.version132"></a>

PostgreSQL version 13\.2 is now available on Amazon RDS\. PostgreSQL contains several improvements that were announced in [PostgreSQL 13\.2](https://www.postgresql.org/docs/release/13.2/)\.

This version also added the following new extensions:
+ The `aws_lambda` extension version 1\.0\. For more information, see [Invoking an AWS Lambda function from an RDS for PostgreSQL DB instance](PostgreSQL-Lambda.md)\. 
+ The [pg\_bigm](https://pgbigm.osdn.jp/pg_bigm_en-1-2.html) extension version 1\.2\. 

For information on all extensions, see [PostgreSQL version 13 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x)\.

#### PostgreSQL version 13\.1 on Amazon RDS<a name="PostgreSQL.Concepts.General.version131"></a>

PostgreSQL version 13\.1 is now available on Amazon RDS\. PostgreSQL contains several improvements that were announced in [PostgreSQL 13\.0](https://www.postgresql.org/docs/13/release-13.html) and [PostgreSQL 13\.1](https://www.postgresql.org/docs/13/release-13-1.html)\.

This version added: 
+ The `bool_plperl` extension version 1\.0\. 
+ The `rds_tools` extension version 1\.0\. For more information, see [ Checking for users with non\-SCRAM passwords ](https://aws.amazon.com/blogs/database/scram-authentication-in-rds-for-postgresql-13/)\. 

For information on all extensions, see [PostgreSQL version 13 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x)\. 

### PostgreSQL 12 versions<a name="PostgreSQL.Concepts.General.version12"></a>

**Topics**
+ [PostgreSQL version 12\.9 on Amazon RDS](#PostgreSQL.Concepts.General.version129)
+ [PostgreSQL version 12\.8 on Amazon RDS](#PostgreSQL.Concepts.General.version128)
+ [PostgreSQL version 12\.7 on Amazon RDS](#PostgreSQL.Concepts.General.version127)
+ [PostgreSQL version 12\.6 on Amazon RDS](#PostgreSQL.Concepts.General.version126)
+ [PostgreSQL version 12\.5 on Amazon RDS](#PostgreSQL.Concepts.General.version125)
+ [PostgreSQL version 12\.4 on Amazon RDS](#PostgreSQL.Concepts.General.version124)
+ [PostgreSQL version 12\.3 on Amazon RDS](#PostgreSQL.Concepts.General.version123)
+ [PostgreSQL version 12\.2 on Amazon RDS](#PostgreSQL.Concepts.General.version122)

#### PostgreSQL version 12\.9 on Amazon RDS<a name="PostgreSQL.Concepts.General.version129"></a>

PostgreSQL version 12\.9 is now available on Amazon RDS\. PostgreSQL version 12\.9 contains several improvements that were announced for PostgreSQL release [12\.9](https://www.postgresql.org/docs/release/12.9/)\. 

This version also includes the following changes:
+  The [pg\_cron](https://github.com/citusdata/pg_cron) extension is updated to 1\.4\.1
+  The [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan/) extension is updated to 1\.3\.7\.

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.8 on Amazon RDS<a name="PostgreSQL.Concepts.General.version128"></a>

PostgreSQL version 12\.8 is now available on Amazon RDS\. PostgreSQL version 12\.8 contains several improvements that were announced for PostgreSQL release [12\.8](https://www.postgresql.org/docs/release/12.8/)\. 

This version also includes the following changes:
+ The [pgrouting](http://docs.pgrouting.org/latest/en/index.html) extension is updated to version 3\.0\.5\.
+ The `pglogical` extension is updated to version 2\.4\.0\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.1\.4, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_raster](https://postgis.net/docs/raster.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.7 on Amazon RDS<a name="PostgreSQL.Concepts.General.version127"></a>

PostgreSQL version 12\.7 is now available on Amazon RDS\. PostgreSQL version 12\.7 contains several improvements that were announced for PostgreSQL release [12\.7](https://www.postgresql.org/docs/release/12.7/)\. 

This version also includes the following changes:
+ The [oracle\_fdw](https://github.com/laurenz/oracle_fdw) extension version 2\.3\.0 is added\. For more information, see [Accessing external data with the oracle\_fdw extension](Appendix.PostgreSQL.CommonDBATasks.md#postgresql-oracle-fdw)\.
+ The [orafce](https://github.com/orafce/orafce) extension is updated to version 3\.15\.
+ The [pg\_cron](PostgreSQL_pg_cron.md) extension is updated to version 1\.3\.1\.
+ The [pg\_partman](PostgreSQL_Partitions.md) extension is updated to version 4\.5\.1\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.0\.3, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_raster](https://postgis.net/docs/raster.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.6 on Amazon RDS<a name="PostgreSQL.Concepts.General.version126"></a>

PostgreSQL version 12\.6 is now available on Amazon RDS\. PostgreSQL version 12\.6 contains several improvements that were announced for PostgreSQL release [12\.6](https://www.postgresql.org/docs/release/12.6/)\. 

This version also includes the following changes:
+ The `aws_lambda` extension version 1\.0 is added\. For more information, see [Invoking an AWS Lambda function from an RDS for PostgreSQL DB instance](PostgreSQL-Lambda.md)\. 
+ The [pg\_bigm](https://pgbigm.osdn.jp/pg_bigm_en-1-2.html) extension version 1\.2 is added\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.0\.2\.

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.5 on Amazon RDS<a name="PostgreSQL.Concepts.General.version125"></a>

PostgreSQL version 12\.5 is now available on Amazon RDS\. PostgreSQL version 12\.5 contains several improvements that were announced for PostgreSQL release [12\.5](https://www.postgresql.org/docs/12/release-12-5.html)\. 

This version also includes the following changes:
+ Added the `pg_partman` extension version 4\.4\.0\. For more information, see [Managing PostgreSQL partitions with the pg\_partman extension](PostgreSQL_Partitions.md)\.
+ Added the `pg_cron` extension version 1\.3\.0\. For more information, see [Scheduling maintenance with the PostgreSQL pg\_cron extension](PostgreSQL_pg_cron.md)\.

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.4 on Amazon RDS<a name="PostgreSQL.Concepts.General.version124"></a>

PostgreSQL version 12\.4 is now available on Amazon RDS\. PostgreSQL version 12\.4 contains several improvements that were announced for PostgreSQL release [12\.4](https://www.postgresql.org/docs/12/release-12-4.html)\. 

This version also includes the following changes:
+ Added the `pg_proctab` extension version 0\.0\.9
+ Added the `rdkit` extension version 3\.8
+ Upgraded the `aws_s3` extension to version 1\.1\.
+ Upgraded the `pglogical` extension to version 2\.3\.2
+ Upgraded the `wal2json` extension to version 2\.3 

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.3 on Amazon RDS<a name="PostgreSQL.Concepts.General.version123"></a>

PostgreSQL version 12\.3 is now available on Amazon RDS\. PostgreSQL version 12\.3 contains several improvements that were announced for PostgreSQL release [12\.3](https://www.postgresql.org/docs/12/release-12-3.html)\. 

This version also includes the following changes:
+ Upgraded the `pg_hint_plan` extension to version 1\.3\.5\.
+ Upgraded the `pglogical` extension to version 2\.3\.1\.

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

#### PostgreSQL version 12\.2 on Amazon RDS<a name="PostgreSQL.Concepts.General.version122"></a>

PostgreSQL version 12\.2 is now available on Amazon RDS\. PostgreSQL version 12\.2 contains several improvements that were announced for PostgreSQL releases [12\.0](https://www.postgresql.org/docs/12/release-12.html), [12\.1](https://www.postgresql.org/docs/12/release-12-1.html), and [12\.2](https://www.postgresql.org/docs/12/release-12-2.html)\. 

For information on all extensions, see [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)\.

### PostgreSQL 11 versions<a name="PostgreSQL.Concepts.General.version11"></a>

**Topics**
+ [PostgreSQL version 11\.14 on Amazon RDS](#PostgreSQL.Concepts.General.version1114)
+ [PostgreSQL version 11\.13 on Amazon RDS](#PostgreSQL.Concepts.General.version1113)
+ [PostgreSQL version 11\.12 on Amazon RDS](#PostgreSQL.Concepts.General.version1112)
+ [PostgreSQL version 11\.11 on Amazon RDS](#PostgreSQL.Concepts.General.version1111)
+ [PostgreSQL version 11\.10 on Amazon RDS](#PostgreSQL.Concepts.General.version1110)
+ [PostgreSQL version 11\.9 on Amazon RDS](#PostgreSQL.Concepts.General.version119)
+ [PostgreSQL version 11\.8 on Amazon RDS](#PostgreSQL.Concepts.General.version118)
+ [PostgreSQL version 11\.7 on Amazon RDS](#PostgreSQL.Concepts.General.version117)
+ [PostgreSQL version 11\.6 on Amazon RDS](#PostgreSQL.Concepts.General.version116)
+ [PostgreSQL version 11\.5 on Amazon RDS](#PostgreSQL.Concepts.General.version115)
+ [PostgreSQL version 11\.4 on Amazon RDS](#PostgreSQL.Concepts.General.version114)
+ [PostgreSQL version 11\.2 on Amazon RDS](#PostgreSQL.Concepts.General.version112)
+ [PostgreSQL version 11\.1 on Amazon RDS](#PostgreSQL.Concepts.General.version111)

#### PostgreSQL version 11\.14 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1114"></a>

PostgreSQL version 11\.14 is now available on Amazon RDS\. PostgreSQL version 11\.14 contains several improvements that were announced for PostgreSQL release [11\.14](https://www.postgresql.org/docs/release/11.14/)\. 

This version also includes the following change:
+  The [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan/) extension is updated to 1\.3\.7\.

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.13 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1113"></a>

PostgreSQL version 11\.13 is now available on Amazon RDS\. PostgreSQL version 11\.13 contains several improvements that were announced for PostgreSQL release [11\.13](https://www.postgresql.org/docs/release/11.13/)\. 

This version also includes the following changes:
+ The [pgrouting](http://docs.pgrouting.org/latest/en/index.html) extension is updated to version 2\.6\.3\.
+ The `pglogical` extension is updated to version 2\.4\.0\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.1\.4, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_raster](https://postgis.net/docs/raster.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.12 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1112"></a>

PostgreSQL version 11\.12 is now available on Amazon RDS\. PostgreSQL version 11\.12 contains several improvements that were announced for PostgreSQL release [11\.12](https://www.postgresql.org/docs/release/11.12/)\. 

This version also includes the following change:
+ The [orafce](https://github.com/orafce/orafce) extension is updated to version 3\.15\.

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.11 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1111"></a>

PostgreSQL version 11\.11 is now available on Amazon RDS\. PostgreSQL version 11\.11 contains several improvements that were announced for PostgreSQL release [11\.11](https://www.postgresql.org/docs/release/11.11/)\. 

This version also added the following new extension:
+ The [pg\_bigm](https://pgbigm.osdn.jp/pg_bigm_en-1-2.html) extension version 1\.2\.

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.10 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1110"></a>

PostgreSQL version 11\.10 is now available on Amazon RDS\. PostgreSQL version 11\.10 contains several improvements that were announced for PostgreSQL release [11\.10](https://www.postgresql.org/docs/11/release-11-10.html)\. 

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.9 on Amazon RDS<a name="PostgreSQL.Concepts.General.version119"></a>

PostgreSQL version 11\.9 is now available on Amazon RDS\. PostgreSQL version 11\.9 contains several improvements that were announced for PostgreSQL release [11\.9](https://www.postgresql.org/docs/11/release-11-9.html)\. 

This version also includes the following changes:
+ Added the `aws_s3` extension version 1\.1
+ Added the `pg_proctab` extension version 0\.0\.9
+ Upgraded the `pgaudit` extension to version 1\.3\.1\.
+ Upgraded the `pglogical` extension to version 2\.2\.2
+ Added the `rdkit` extension version 3\.8

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.8 on Amazon RDS<a name="PostgreSQL.Concepts.General.version118"></a>

PostgreSQL version 11\.8 contains several bug fixes for issues in release 11\.7\. For more information on the fixes in PostgreSQL 11\.8, see the [PostgreSQL 11\.8 documentation](https://www.postgresql.org/docs/11/release-11-8.html)\. 

This version also includes the following change:
+ Upgraded the `pg_hint_plan` extension to version 1\.3\.5\.

For information on all extensions, see [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)\.

#### PostgreSQL version 11\.7 on Amazon RDS<a name="PostgreSQL.Concepts.General.version117"></a>

PostgreSQL version 11\.7 contains several bug fixes for issues in release 11\.6\. For more information on the fixes in PostgreSQL 11\.7, see the [PostgreSQL 11\.7 documentation](https://www.postgresql.org/docs/11/release-11-7.html)\. 

#### PostgreSQL version 11\.6 on Amazon RDS<a name="PostgreSQL.Concepts.General.version116"></a>

PostgreSQL version 11\.6 contains several bug fixes for issues in release 11\.5\. For more information on the fixes in PostgreSQL 11\.6, see the [PostgreSQL documentation](https://www.postgresql.org/docs/11/release-11-6.html)\. 

This version also includes the following changes:
+ Upgraded the `pgTAP` extension to version 1\.1\.0\.
+ Added the `plprofiler` extension\.
+ Added to `shared_preload_libraries` support for `pg_prewarm` to start automatically\.

#### PostgreSQL version 11\.5 on Amazon RDS<a name="PostgreSQL.Concepts.General.version115"></a>

PostgreSQL version 11\.5 contains several bug fixes for issues in release 11\.4\. For more information on the fixes in PostgreSQL 11\.5, see the [PostgreSQL documentation](https://www.postgresql.org/docs/11/release-11-5.html)\. 

This version also includes the following changes:
+ A new extension `pg_transport` is added\.
+ The extension `aws_s3` has been updated to support virtual\-hosted style requests\. For more information, see [Amazon S3 path deprecation plan – The rest of the story](http://aws.amazon.com/blogs/aws/amazon-s3-path-deprecation-plan-the-rest-of-the-story/)\. 
+ The `PostGIS` extension is updated to version 2\.5\.2\.

#### PostgreSQL version 11\.4 on Amazon RDS<a name="PostgreSQL.Concepts.General.version114"></a>

This release contains an important security fix and also bug fixes and improvements done by the PostgreSQL community\. For more information on the security fix, see the [PostgreSQL community announcement](https://www.postgresql.org/about/news/1949/) and the security fix CVE\-2019\-10164\. 

With this release, the `pg_hint_plan` extension has been updated to version 1\.3\.4\.

For more information on the fixes in PostgreSQL 11\.4, see the [PostgreSQL documentation](https://www.postgresql.org/docs/11/release-11-4.html)\.

#### PostgreSQL version 11\.2 on Amazon RDS<a name="PostgreSQL.Concepts.General.version112"></a>

PostgreSQL version 11\.2 contains several bug fixes for issues in release 11\.1\. For more information on the fixes in PostgreSQL 11\.2, see the [PostgreSQL documentation](https://www.postgresql.org/docs/11/release-11-2.html)\.

This version also includes the following changes:
+ A new [pgTAP](https://pgtap.org/) extension version 1\.0\.
+ Support for Amazon S3 import\. For more information, see [Importing Amazon S3 data into an RDS for PostgreSQL DB instance](USER_PostgreSQL.S3Import.md)\.
+ Multiple major version upgrade is available to PostgreSQL 11\.2 from certain previous PostgreSQL versions\. For more information, see [ Choosing a major version upgrade for PostgreSQL ](USER_UpgradeDBInstance.PostgreSQL.md#USER_UpgradeDBInstance.PostgreSQL.MajorVersion)\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 11\.1 on Amazon RDS<a name="PostgreSQL.Concepts.General.version111"></a>

PostgreSQL version 11\.1 contains several improvements that were announced in [PostgreSQL 11\.1 released\!](https://www.postgresql.org/about/news/1905/) This version includes SQL stored procedures that enable embedded transactions within a procedure\. This version also includes major improvements to partitioning and parallelism and many useful performance improvements\. For example, by using a non\-null constant for a column default, you can now use an ALTER TABLE command to add a column without causing a table rewrite\.

PostgreSQL version 11\.1 contains several bug fixes for issues in release 11\. For complete details, see the [PostgreSQL release 11\.1 documentation](https://www.postgresql.org/docs/11/release-11-1.html)\. Some changes in this version include the following:
+ Partitioning – Partitioning improvements include support for hash partitioning, enabling creation of a default partition, and dynamic row movement to another partition based on the key column update\.
+ Performance – Performance improvements include parallelism while creating indexes, materialized views, hash joins, and sequential scans to make the operations perform better\.
+ Stored procedures – SQL stored procedures now added support embedded transactions\.
+ Support for Just\-In\-Time \(JIT\) capability – RDS for PostgreSQL 11 instances are created with JIT capability, speeding evaluation of expressions\. To enable JIT capability, set the `jit` parameter to 1 in the PostgreSQL parameter group for the database\. 
+ Segment size – The write\-ahead logging \(WAL\) segment size has been changed from 16 MB to 64 MB\.
+ Autovacuum improvements – To provide valuable logging, the parameter `rds.force_autovacuum_logging` is ON by default in conjunction with the `log_autovacuum_min_duration` parameter set to 10 seconds\. To increase autovacuum effectiveness, the values for the `autovacuum_max_workers` and `autovacuum_vacuum_cost_limit` parameters are computed based on host memory capacity to provide larger default values\.
+ Improved transaction timeout – The parameter `idle_in_transaction_session_timeout` is set to 24 hours\. Any session that has been idle more than 24 hours is terminated\.
+ Performance metrics – The `pg_stat_statements` extension is included in `shared_preload_libraries` by default\. This avoids having to reboot the instance immediately after creation\. However, this functionality still requires you to run the statement `CREATE EXTENSION pg_stat_statements;`\. Also, `track_io_timing` is enabled by default to add more granular data to `pg_stat_statements`\.
+ The tsearch2 extension is no longer supported – If your application uses `tsearch2` functions, update it to use the equivalent functions provided by the core PostgreSQL engine\. For more information about the tsearch2 extension, see [PostgreSQL tsearch2](https://www.postgresql.org/docs/9.6/static/tsearch2.html)\.
+ The chkpass extension is no longer supported – For more information about the `chkpass` extension, see [PostgreSQL chkpass](https://www.postgresql.org/docs/10/chkpass.html)\.
+ Extension updates for RDS for PostgreSQL 11\.1 include the following: 
  + `pgaudit` is updated to 1\.3\.0\.
  + `pg_hint_plan` is updated to 1\.3\.2\.
  + `pglogical` is updated to 2\.2\.1\.
  + `plcoffee` is updated to 2\.3\.8\.
  + `plv8` is updated to 2\.3\.8\.
  + `PostGIS` is updated to 2\.5\.1\.
  + `prefix` is updated to 1\.2\.8\.
  + `wal2json` is updated to hash 9e962bad\.

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

### PostgreSQL 10 versions<a name="PostgreSQL.Concepts.General.version10"></a>

**Topics**
+ [PostgreSQL version 10\.19 on Amazon RDS](#PostgreSQL.Concepts.General.version1019)
+ [PostgreSQL version 10\.18 on Amazon RDS](#PostgreSQL.Concepts.General.version1018)
+ [PostgreSQL version 10\.17 on Amazon RDS](#PostgreSQL.Concepts.General.version1017)
+ [PostgreSQL version 10\.16 on Amazon RDS](#PostgreSQL.Concepts.General.version1016)
+ [PostgreSQL version 10\.15 on Amazon RDS](#PostgreSQL.Concepts.General.version1015)
+ [PostgreSQL version 10\.14 on Amazon RDS](#PostgreSQL.Concepts.General.version1014)
+ [PostgreSQL version 10\.13 on Amazon RDS](#PostgreSQL.Concepts.General.version1013)
+ [PostgreSQL version 10\.12 on Amazon RDS](#PostgreSQL.Concepts.General.version1012)
+ [PostgreSQL version 10\.11 on Amazon RDS](#PostgreSQL.Concepts.General.version1011)
+ [PostgreSQL version 10\.10 on Amazon RDS](#PostgreSQL.Concepts.General.version1010)
+ [PostgreSQL version 10\.9 on Amazon RDS](#PostgreSQL.Concepts.General.version109)
+ [PostgreSQL version 10\.7 on Amazon RDS](#PostgreSQL.Concepts.General.version107)
+ [PostgreSQL version 10\.6 on Amazon RDS](#PostgreSQL.Concepts.General.version106)
+ [PostgreSQL version 10\.5 on Amazon RDS](#PostgreSQL.Concepts.General.version105)
+ [PostgreSQL version 10\.4 on Amazon RDS](#PostgreSQL.Concepts.General.version104)
+ [PostgreSQL version 10\.3 on Amazon RDS](#PostgreSQL.Concepts.General.version103)
+ [PostgreSQL version 10\.1 on Amazon RDS](#PostgreSQL.Concepts.General.version101)

#### PostgreSQL version 10\.19 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1019"></a>

PostgreSQL version 10\.19 is now available on Amazon RDS\. PostgreSQL version 10\.19 contains several improvements that were announced for PostgreSQL release [10\.19](https://www.postgresql.org/docs/release/10.19/)\. 

This version also includes the following change:
+  The [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan/) extension is updated to 1\.3\.6\.

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.18 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1018"></a>

PostgreSQL version 10\.18 is now available on Amazon RDS\. PostgreSQL version 10\.18 contains several improvements that were announced for PostgreSQL release [10\.18](https://www.postgresql.org/docs/release/10.18/)\. 

This version also includes the following changes:
+ The [pgrouting](http://docs.pgrouting.org/latest/en/index.html) extension is updated to version 2\.5\.5\.
+ The `pglogical` extension is updated to version 2\.4\.0\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 3\.1\.4, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_raster](https://postgis.net/docs/raster.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.17 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1017"></a>

PostgreSQL version 10\.17 is now available on Amazon RDS\. PostgreSQL version 10\.17 contains several improvements that were announced for PostgreSQL release [10\.17](https://www.postgresql.org/docs/release/10.17/)\.

This version also includes the following change:
+ The [orafce](https://github.com/orafce/orafce) extension is updated to version 3\.15\.

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.16 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1016"></a>

PostgreSQL version 10\.16 is now available on Amazon RDS\. PostgreSQL version 10\.16 contains several improvements that were announced for PostgreSQL release [10\.16](https://www.postgresql.org/docs/release/10.16/)\. 

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.15 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1015"></a>

PostgreSQL version 10\.15 is now available on Amazon RDS\. PostgreSQL version 10\.15 contains several improvements that were announced for PostgreSQL release [10\.15](https://www.postgresql.org/docs/10/release-10-15.html)\. 

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.14 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1014"></a>

PostgreSQL version 10\.14 is now available on Amazon RDS\. PostgreSQL version 10\.14 contains several improvements that were announced for PostgreSQL release [10\.14](https://www.postgresql.org/docs/10/release-10-14.html)\. 

This version also includes the following changes:
+ Added the `aws_s3` extension version 1\.1\. For more information, see [Exporting data from an RDS for PostgreSQL DB instance to Amazon S3](postgresql-s3-export.md)\.
+ Upgraded the `pgaudit` extension to version 1\.2\.1
+ Upgraded the `pglogical` extension to version 2\.2\.2
+ Upgraded the `wal2json` extension to version 2\.3

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.13 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1013"></a>

PostgreSQL version 10\.13 contains several bug fixes for issues in release 10\.12\. For more information on the fixes in PostgreSQL 10\.13, see the [PostgreSQL 10\.13 documentation](https://www.postgresql.org/docs/10/release-10-13.html)\. 

This version also includes the following change:
+ Upgraded the `pg_hint_plan` extension to version 1\.3\.5\.

For information on all extensions, see [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)\.

#### PostgreSQL version 10\.12 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1012"></a>

PostgreSQL version 10\.12 contains several bug fixes for issues in release 10\.11\. For more information on the fixes in PostgreSQL 10\.12, see the [PostgreSQL 10\.12 documentation](https://www.postgresql.org/docs/10/release-10-12.html)\. 

#### PostgreSQL version 10\.11 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1011"></a>

PostgreSQL version 10\.11 contains several bug fixes for issues in release 10\.10\. For more information on the fixes in PostgreSQL 10\.11, see the [PostgreSQL documentation](https://www.postgresql.org/docs/10/release-10-11.html)\. Changes in this version include the following:
+ Added the `plprofiler` extension\.

#### PostgreSQL version 10\.10 on Amazon RDS<a name="PostgreSQL.Concepts.General.version1010"></a>

PostgreSQL version 10\.10 contains several bug fixes for issues in release 10\.9\. For more information on the fixes in PostgreSQL 10\.10, see the [PostgreSQL documentation](https://www.postgresql.org/docs/10/release-10-10.html)\. Changes in this version include the following:
+ The `aws_s3` extension is updated to support virtual\-hosted style requests\. For more information, see [Amazon S3 path deprecation plan – The rest of the story](http://aws.amazon.com/blogs/aws/amazon-s3-path-deprecation-plan-the-rest-of-the-story/)\. 
+ The `PostGIS` extension is updated to version 2\.5\.2\.



#### PostgreSQL version 10\.9 on Amazon RDS<a name="PostgreSQL.Concepts.General.version109"></a>

This release contains an important security fix and also bug fixes and improvements done by the PostgreSQL community\. For more information on the security fix, see the [PostgreSQL community announcement](https://www.postgresql.org/about/news/1949/) and [security fix CVE\-2019\-10164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2019-10164)\. 

With this release, the `pg_hint_plan` extension has been updated to version 1\.3\.3\.

For more information on the fixes in PostgreSQL 10\.9, see the [PostgreSQL documentation](https://www.postgresql.org/docs/10/release-10-9.html)\.

#### PostgreSQL version 10\.7 on Amazon RDS<a name="PostgreSQL.Concepts.General.version107"></a>

PostgreSQL version 10\.7 contains several bug fixes for issues in release 10\.6\. For more information on the fixes in 10\.7, see the [PostgreSQL documentation](https://www.postgresql.org/docs/10/release-10-7.html)\.

This version also includes the following changes:
+ Support for Amazon S3 import\. For more information, see [Importing Amazon S3 data into an RDS for PostgreSQL DB instance](USER_PostgreSQL.S3Import.md)\.
+ Multiple major version upgrade is available to PostgreSQL 10\.7 from certain previous PostgreSQL versions\. For more information, see [ Choosing a major version upgrade for PostgreSQL ](USER_UpgradeDBInstance.PostgreSQL.md#USER_UpgradeDBInstance.PostgreSQL.MajorVersion)\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

#### PostgreSQL version 10\.6 on Amazon RDS<a name="PostgreSQL.Concepts.General.version106"></a>

PostgreSQL version 10\.6 contains several bug fixes for issues in release 10\.5\. For more information on the fixes in PostgreSQL 10\.6, see the [PostgreSQL documentation](http://www.postgresql.org/docs/10/static/release-10-6.html)\.

This version also includes the following changes:
+ A new `rds.restrict_password_commands` parameter and a new `rds_password` role have been introduced\. When the `rds.restrict_password_commands` parameter is enabled, only users who have the `rds_password` role can make user password and password expiration changes\. By restricting password\-related operations to a limited set of roles, you can implement policies such as password complexity requirements from the client side\. The `rds.restrict_password_commands` parameter is static, so it requires a database restart to change it\. For more information, see [Restricting password management](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.RestrictPasswordMgmt)\. 
+ The logical decoding plugin `wal2json` has been updated to commit `9e962ba`\. 

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

**Note**  
Amazon RDS for PostgreSQL has announced the removal of the `tsearch2` extension in the next major release\. We encourage customers still using pre\-8\.3 text search to migrate to the equivalent built\-in features\. For more information about migrating, see the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/static/textsearch-migration.html)\. 

#### PostgreSQL version 10\.5 on Amazon RDS<a name="PostgreSQL.Concepts.General.version105"></a>

PostgreSQL version 10\.5 contains several bug fixes for issues in release 10\.4\. For more information on the fixes in 10\.5, see the [PostgreSQL documentation](http://www.postgresql.org/docs/10/static/release-10-5.html)\.

This version also includes the following changes:
+ Support for the `pglogical` extension version 2\.2\.0\. Prerequisites for using this extension are the same as the prerequisites for using logical replication for PostgreSQL as described in [Logical replication for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.LogicalReplication)\.
+ Support for the `pg_similarity` extension version 1\.0\.
+ Support for the `pageinspect` extension version 1\.6\.
+ Support for the `libprotobuf` extension version 1\.3\.0 for the PostGIS component\.
+ An update for the `pg_hint_plan` extension to version 1\.3\.1\.
+ An update for the `wal2json` extension to version 01c5c1e\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 10\.4 on Amazon RDS<a name="PostgreSQL.Concepts.General.version104"></a>

PostgreSQL version 10\.4 contains several bug fixes for issues in release 10\.3\. For more information on the fixes in 10\.4, see the [PostgreSQL documentation](http://www.postgresql.org/docs/10/static/release-10-4.html)\.

This version also includes the following changes:
+ Support for PostgreSQL 10 Logical Replication using the native publication and subscription framework\. RDS for PostgreSQL databases can function as both publishers and subscribers\. You can specify replication to other PostgreSQL databases at the database\-level or at the table\-level\. With logical replication, the publisher and subscriber databases need not be physically identical \(block\-to\-block\) to each other\. This allows for use cases such as data consolidation, data distribution, and data replication across different database versions for 10\.4 and above\. For more details, refer to [Logical replication for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.LogicalReplication)\.
+ The temporary file size limitation is user\-configurable\. You require the **rds\_superuser** role to modify the `temp_file_limit` parameter\.
+ Update of the `GDAL` library, which is used by the PostGIS extension\. See [Working with the PostGIS extension](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md)\.
+ Update of the `ip4r` extension to version 2\.1\.1\.
+ Update of the `pg_repack` extension to version 1\.4\.3\. See [Working with the pg\_repack extension](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.pg_repack)\.
+ Update of the `plv8` extension to version 2\.1\.2\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

**Note**  
The `tsearch2` extension is to be removed in the next major release\. We encourage customers still using pre\-8\.3 text search to migrate to the equivalent built\-in features\. For more information about migrating, see the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/static/textsearch-migration.html)\.

#### PostgreSQL version 10\.3 on Amazon RDS<a name="PostgreSQL.Concepts.General.version103"></a>

PostgreSQL version 10\.3 contains several bug fixes for issues in release 10\. For more information on the fixes in 10\.3, see the [PostgreSQL documentation](http://www.postgresql.org/docs/10/static/release-10-3.html)\.

Version 2\.1\.0 of plv8 is now available\. If you use plv8 and upgrade PostgreSQL to a new plv8 version, you immediately take advantage of the new extension but the catalog metadata doesn't reflect this fact\. For the steps to synchronize your catalog metadata with the new version of plv8, see [Upgrading PLV8 ](#PostgreSQL.Concepts.General.UpgradingPLv8)\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 10\.1 on Amazon RDS<a name="PostgreSQL.Concepts.General.version101"></a>

PostgreSQL version 10\.1 contains several bug fixes for issues in release 10\. For more information on the fixes in 10\.1, see the [PostgreSQL documentation](http://www.postgresql.org/docs/10/static/release-10-1.html) and the [PostgreSQL 10 community announcement](https://www.postgresql.org/about/news/1786/)\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

PostgreSQL version 10\.1 includes the following changes: 
+ **Declarative table partitioning** – PostgreSQL 10 adds table partitioning to SQL syntax and native tuple routing\. 
+ **Parallel queries** – When you create a new PostgreSQL 10\.1 instance, parallel queries are enabled for the `default.postgres10` parameter group\. The parameter [max\_parallel\_workers\_per\_gather](https://www.postgresql.org/docs/10/static/runtime-config-resource.html#GUC-MAX-PARALLEL-WORKERS-PER-GATHER) is set to 2 by default, but you can modify it to support your specific workload requirements\.
+ **Support for the international components for unicode \(ICU\)** – You can use the ICU library to provide explicitly versioned collations\. Amazon RDS for PostgreSQL 10\.1 is compiled with ICU version 60\.2\. For more information about ICU implementation in PostgreSQL, see [Collation support](https://www.postgresql.org/docs/10/static/collation.html)\.
+ **Huge pages** – Huge pages is a feature of the Linux kernel that uses multiple page size capabilities of modern hardware architectures\. Amazon RDS for PostgreSQL supports huge pages with a global configuration parameter\. When you create a new PostgreSQL 10\.1 instance with RDS, the `huge_pages` parameter is set to `"on"` for the` default.postgres10` parameter group\. You can modify this setting to support your specific workload requirements\. 
+ Extension **plv8 update** – plv8 is a procedural language that you can use to write functions in JavaScript that you can then call from SQL\. This release of PostgreSQL supports version 2\.1\.0 of plv8\.
+ **Renaming of xlog and location** – In PostgreSQL version 10 the abbreviation "xlog" has changed to "wal", and the term "location" has changed to "lsn"\. For more information, see [ https://www\.postgresql\.org/docs/10/static/release\-10\.html\#id\-1\.11\.6\.8\.4](https://www.postgresql.org/docs/10/static/release-10.html#id-1.11.6.8.4)\. 
+ **tsearch2 extension** – Amazon RDS continues to provide the `tsearch2` extension in PostgreSQL version 10, but is to remove it in the next major version release\. If your application uses tsearch2 functions update it to use the equivalent functions the core engine provides\. For more information see [tsearch2](https://www.postgresql.org/docs/9.6/static/tsearch2.html) in the PostgreSQL documentation\.

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

### PostgreSQL 9\.6 versions<a name="PostgreSQL.Concepts.General.version96"></a>

RDS for PostgreSQL 9\.6 will be deprecated on April 26, 2022\. For more information about version 9\.6 deprecation, see [Deprecation of PostgreSQL version 9\.6](#PostgreSQL.Concepts.General.DBVersions.Deprecation96)\. 

**Topics**
+ [PostgreSQL version 9\.6\.24 on Amazon RDS](#PostgreSQL.Concepts.General.version9624)
+ [PostgreSQL version 9\.6\.23 on Amazon RDS](#PostgreSQL.Concepts.General.version9623)
+ [PostgreSQL version 9\.6\.22 on Amazon RDS](#PostgreSQL.Concepts.General.version9622)
+ [PostgreSQL version 9\.6\.21 on Amazon RDS](#PostgreSQL.Concepts.General.version9621)
+ [PostgreSQL version 9\.6\.20 on Amazon RDS](#PostgreSQL.Concepts.General.version9620)
+ [PostgreSQL version 9\.6\.19 on Amazon RDS](#PostgreSQL.Concepts.General.version9619)
+ [PostgreSQL version 9\.6\.18 on Amazon RDS](#PostgreSQL.Concepts.General.version9618)
+ [PostgreSQL version 9\.6\.17 on Amazon RDS](#PostgreSQL.Concepts.General.version9617)
+ [PostgreSQL version 9\.6\.16 on Amazon RDS](#PostgreSQL.Concepts.General.version9616)
+ [PostgreSQL version 9\.6\.15 on Amazon RDS](#PostgreSQL.Concepts.General.version9615)
+ [PostgreSQL version 9\.6\.14 on Amazon RDS](#PostgreSQL.Concepts.General.version9614)
+ [PostgreSQL version 9\.6\.12 on Amazon RDS](#PostgreSQL.Concepts.General.version9612)
+ [PostgreSQL version 9\.6\.11 on Amazon RDS](#PostgreSQL.Concepts.General.version9611)
+ [PostgreSQL version 9\.6\.10 on Amazon RDS](#PostgreSQL.Concepts.General.version9610)
+ [PostgreSQL version 9\.6\.9 on Amazon RDS](#PostgreSQL.Concepts.General.version969)
+ [PostgreSQL version 9\.6\.8 on Amazon RDS](#PostgreSQL.Concepts.General.version968)
+ [PostgreSQL version 9\.6\.6 on Amazon RDS](#PostgreSQL.Concepts.General.version966)
+ [PostgreSQL version 9\.6\.5 on Amazon RDS](#PostgreSQL.Concepts.General.version965)
+ [PostgreSQL version 9\.6\.3 on Amazon RDS](#PostgreSQL.Concepts.General.version963)
+ [PostgreSQL version 9\.6\.2 on Amazon RDS](#PostgreSQL.Concepts.General.version962)
+ [PostgreSQL version 9\.6\.1 on Amazon RDS](#PostgreSQL.Concepts.General.version961)

#### PostgreSQL version 9\.6\.24 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9624"></a>

PostgreSQL version 9\.6\.24 is now available on Amazon RDS\. PostgreSQL version 9\.6\.24 contains several improvements that were announced for PostgreSQL release [9\.6\.24](https://www.postgresql.org/docs/release/9.6.24/)\. 

This version also includes the following change:
+  The [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan/) extension is updated to 1\.2\.7\.

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.23 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9623"></a>

PostgreSQL version 9\.6\.23 is now available on Amazon RDS\. PostgreSQL version 9\.6\.23 contains several improvements that were announced for PostgreSQL release [9\.6\.23](https://www.postgresql.org/docs/release/9.6.23/)\. 

This version also includes the following changes:
+ The `pglogical` extension is updated to version 2\.4\.0\.
+ The [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md#CHAP_PostgreSQL.Extensions.PostGIS) extension is updated to version 2\.5\.5, along with the following related extensions:
  + [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html)
  + [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html)
  + [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html)
  + [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html)

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.22 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9622"></a>

PostgreSQL version 9\.6\.22 is now available on Amazon RDS\. PostgreSQL version 9\.6\.22 contains several improvements that were announced for PostgreSQL release [9\.6\.22](https://www.postgresql.org/docs/release/9.6.22/)\. 

This version also includes the following change:
+ The [orafce](https://github.com/orafce/orafce) extension is updated to version 3\.15\.

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.21 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9621"></a>

PostgreSQL version 9\.6\.21 is now available on Amazon RDS\. PostgreSQL version 9\.6\.21 contains several improvements that were announced for PostgreSQL release [9\.6\.21](https://www.postgresql.org/docs/release/9.6.21/)\. 

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.20 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9620"></a>

PostgreSQL version 9\.6\.20 is now available on Amazon RDS\. PostgreSQL version 9\.6\.20 contains several improvements that were announced for PostgreSQL release [9\.6\.20](https://www.postgresql.org/docs/9.6/release-9-6-20.html)\. 

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.19 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9619"></a>

PostgreSQL version 9\.6\.19 is now available on Amazon RDS\. PostgreSQL version 9\.6\.19 contains several improvements that were announced for PostgreSQL release [9\.6\.19](https://www.postgresql.org/docs/9.6/release-9-6-19.html)\. 

This version also includes the following changes:
+ Upgraded the `pgaudit` extension to version 1\.1\.2
+ Upgraded the `pglogical` extension to version 2\.2\.2
+ Upgraded the `wal2json` extension to version 2\.3

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.18 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9618"></a>

PostgreSQL version 9\.6\.18 contains several bug fixes for issues in release 9\.6\.17\. For more information on the fixes in PostgreSQL 9\.6\.18, see the [PostgreSQL 9\.6\.18 documentation](https://www.postgresql.org/docs/9.6/release-9-6-18.html)\. 

This version also includes the following change:
+ Upgraded the `pg_hint_plan` extension to version 1\.2\.6\.

For information on all extensions, see [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)\.

#### PostgreSQL version 9\.6\.17 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9617"></a>

PostgreSQL version 9\.6\.17 contains several bug fixes for issues in release 9\.6\.16\. For more information on the fixes in PostgreSQL 9\.6\.17, see the [PostgreSQL 9\.6\.17 documentation](https://www.postgresql.org/docs/9.6/release-9-6-17.html)\. 

#### PostgreSQL version 9\.6\.16 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9616"></a>

PostgreSQL version 9\.6\.16 contains several bug fixes for issues in release 9\.6\.15\. For more information on the fixes in PostgreSQL 9\.6\.16, see the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/release-9-6-16.html)\. 

#### PostgreSQL version 9\.6\.15 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9615"></a>

PostgreSQL version 9\.6\.15 contains several bug fixes for issues in release 9\.6\.14\. For more information on the fixes in PostgreSQL 9\.6\.15, see the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/release-9-6-15.html)\. 

The `PostGIS` extension is updated to version 2\.5\.2\.

#### PostgreSQL version 9\.6\.14 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9614"></a>

This release contains bug fixes and improvements done by the PostgreSQL community\. 

With this release, the `pg_hint_plan` extension has been updated to version 1\.2\.5\.

For more information on the fixes in PostgreSQL 9\.6\.14, see the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/release-9-6-14.html)\.

#### PostgreSQL version 9\.6\.12 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9612"></a>

PostgreSQL version 9\.6\.12 contains several bug fixes for issues in release 9\.6\.11\. For more information on the fixes in 9\.6\.12, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/release-9-6-12.html)\. 

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

#### PostgreSQL version 9\.6\.11 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9611"></a>

PostgreSQL version 9\.6\.11 contains several bug fixes for issues in release 9\.6\.10\. For more information on the fixes in PostgreSQL 9\.6\.11, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/static/release-9-6-11.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

With this version, the logical decoding plugin `wal2json` has been updated to commit `9e962ba`\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 9\.6\.10 on Amazon RDS<a name="PostgreSQL.Concepts.General.version9610"></a>

PostgreSQL version 9\.6\.10 contains several bug fixes for issues in release 9\.6\.9\. For more information on the fixes in 9\.6\.10, see the [PostgreSQL documentation](http://www.postgresql.org/docs/current/static/release-9-6-10.html)\. 

This version includes the following changes: 
+ Support for the `pglogical` extension version 2\.2\.0\. Prerequisites for using this extension are the same as the prerequisites for using logical replication for PostgreSQL as described in [Logical replication for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.LogicalReplication)\. 
+ Support for the `pg_similarity` extension version 2\.2\.0\.
+ An update for the `wal2json` extension to version 01c5c1e\.
+ An update for the `pg_hint_plan` extension to version 1\.2\.3\.

For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 9\.6\.9 on Amazon RDS<a name="PostgreSQL.Concepts.General.version969"></a>

PostgreSQL version 9\.6\.9 contains several bug fixes for issues in release 9\.6\.8\. For more information on the fixes in 9\.6\.9, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/static/release-9-6-9.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

This version includes the following changes: 
+ The temporary file size limitation is user\-configurable\. You require the **rds\_superuser** role to modify the `temp_file_limit` parameter\.
+ Update of the `GDAL` library, which is used by the PostGIS extension\. See [Working with the PostGIS extension](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md)\.
+ Update of the `ip4r` extension to version 2\.1\.1\.
+ Update of the `pgaudit` extension to version 1\.1\.1\. See [Working with the pgaudit extension](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.pgaudit)\.

  Update of the `pg_repack` extension to version 1\.4\.3\. See [Working with the pg\_repack extension](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.pg_repack)\.
+ Update of the `plv8` extension to version 2\.1\.2\.

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 9\.6\.8 on Amazon RDS<a name="PostgreSQL.Concepts.General.version968"></a>

PostgreSQL version 9\.6\.8 contains several bug fixes for issues in release 9\.6\.6\. For more information on the fixes in 9\.6\.8, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/static/release-9-6-8.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 9\.6\.6 on Amazon RDS<a name="PostgreSQL.Concepts.General.version966"></a>

PostgreSQL version 9\.6\.6 contains several bug fixes for issues in release 9\.6\.5\. For more information on the fixes in 9\.6\.6, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/static/release-9-6-6.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

This version includes the following features: 
+ Supports the `orafce` extension, version 3\.6\.1\. This extension contains functions that are native to commercial databases, and can be helpful if you are porting a commercial database to PostgreSQL\. For more information about using `orafce` with Amazon RDS, see [Working with the orafce extension](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.orafce)\.
+ Supports the `prefix` extension, version 1\.2\.6\. This extension provides an operator for text prefix searches\. For more information about `prefix`, see the [prefix project on GitHub](https://github.com/dimitri/prefix)\.
+ Supports version 2\.3\.4 of PostGIS, version 2\.4\.2 of pgrouting, and an updated version of wal2json\.

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 9\.6\.5 on Amazon RDS<a name="PostgreSQL.Concepts.General.version965"></a>

PostgreSQL version 9\.6\.5 contains several bug fixes for issues in release 9\.6\.4\. For more information on the fixes in 9\.6\.5, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/static/release-9-6-5.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

This version also includes support for the [pgrouting](http://pgrouting.org/), [postgresql\-hll](https://github.com/citusdata/postgresql-hll/releases/tag/v2.10.2) extensions, and the [decoder\_raw](https://github.com/michaelpq/pg_plugins/tree/master/decoder_raw) optional extension\.

For the complete list of extensions supported by Amazon RDS for PostgreSQL, see [PostgreSQL extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions)\.

#### PostgreSQL version 9\.6\.3 on Amazon RDS<a name="PostgreSQL.Concepts.General.version963"></a>

PostgreSQL version 9\.6\.3 contains several new features and bug fixes\. This version includes the following features: 
+ Supports the extension `pg_repack` version 1\.4\.0\. You can use this extension to remove bloat from tables and indexes\. For more information on using `pg_repack` with Amazon RDS, see [Working with the pg\_repack extension](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.pg_repack)\.
+ Supports the extension `pgaudit` version 1\.1\.0\. This extension provides detailed session and object audit logging\. For more information on using pgaudit with Amazon RDS, see [Working with the pgaudit extension](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.pgaudit)\.
+ Supports `wal2json`, an output plugin for logical decoding\.
+ Supports the `auto_explain` extension\. You can use this extension to log execution plans of slow statements automatically\. The following example shows how to use `auto_explain` from within an Amazon RDS PostgreSQL session:

  ```
  LOAD '$libdir/plugins/auto_explain';
  ```

  For more information on using `auto_explain`, see the [ PostgreSQL documentation](https://www.postgresql.org/docs/current/static/auto-explain.html)\. 

#### PostgreSQL version 9\.6\.2 on Amazon RDS<a name="PostgreSQL.Concepts.General.version962"></a>

PostgreSQL version 9\.6\.2 contains several new features and bug fixes\. The new version also includes the following extension versions: 
+ PostGIS version 2\.3\.2
+ [ pg\_freespacemap](https://www.postgresql.org/docs/current/static/pgfreespacemap.html) version 1\.1–Provides a way to examine the free space map \(FSM\)\. This extension provides an overloaded function called pg\_freespace\. The functions show the value recorded in the free space map for a given page, or for all pages in the relation\.
+ [pg\_hint\_plan](http://pghintplan.osdn.jp/pg_hint_plan.html) version 1\.1\.3– Provides control of execution plans by using hinting phrases at the beginning of SQL statements\.
+ log\_fdw version 1\.0–Using this extension from Amazon RDS, you can load and query your database engine log from within the database\. For more information, see [Using the log\_fdw extension](#CHAP_PostgreSQL.Extensions.log_fdw)\.
+ With this version release, you can now edit the `max_worker_processes` parameter in a DB parameter group\. 

PostgreSQL version 9\.6\.2 on Amazon RDS also supports altering enum values\. For more information, see [ALTER ENUM for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.AlterEnum)\.

 For more information on the fixes in 9\.6\.2, see the [PostgreSQL documentation](http://www.postgresql.org/docs/9.6/static/release-9-6-2.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. 

#### PostgreSQL version 9\.6\.1 on Amazon RDS<a name="PostgreSQL.Concepts.General.version961"></a>

PostgreSQL version 9\.6\.1 contains several new features and improvements\. For more information about the fixes and improvements in PostgreSQL 9\.6\.1, see the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/static/release-9-6-1.html)\. For information on upgrading the engine version for your PostgreSQL DB instance, see [Upgrading the PostgreSQL DB engine for Amazon RDS](USER_UpgradeDBInstance.PostgreSQL.md)\. For information about performing parallel queries and phrase searching using Amazon RDS for PostgreSQL 9\.6\.1, see the [AWS database blog](http://aws.amazon.com/blogs/database/performing-parallel-queries-and-phrase-searching-with-amazon-rds-for-postgresql-9-6-1/)\.

PostgreSQL version 9\.6\.1 includes the following changes:
+ **Parallel query processing**: Supports parallel processing of large read\-only queries, allowing sequential scans, hash joins, nested loops, and aggregates to be run in parallel\. By default, parallel query processing is not enabled\. To enable parallel query processing, set the parameter `max_parallel_workers_per_gather` to a value larger than zero\.
+ **Updated postgres\_fdw extension**: Supports remote JOINs, SORTs, UPDATEs, and DELETE operations\.
+ **plv8 update**: Provides version 1\.5\.3 of the plv8 language\.
+ **PostGIS version update**: Supports POSTGIS="2\.3\.0 r15146" GEOS="3\.5\.0\-CAPI\-1\.9\.0 r4084" PROJ="Rel\. 4\.9\.2, 08 September 2015" GDAL="GDAL 2\.1\.1, released 2016/07/07" LIBXML="2\.9\.1" LIBJSON="0\.12" RASTER
+ **Vacuum improvement**: Avoids scanning pages unnecessarily during vacuum freeze operations\.
+ **Full\-text search support for phrases**: Supports the ability to specify a phrase\-search query in tsquery input using the new operators <\-> and <N>\.
+ **Two new extensions are supported**:
  + `bloom`, an index access method based on [Bloom filters](http://en.wikipedia.org/wiki/Bloom_filter)
  + `pg_visibility`, which provides a means for examining the visibility map and page\-level visibility information of a table\.
+ With the release of version 9\.6\.2, you can now edit the `max_worker_processes` parameter in a PostgreSQL version 9\.6\.1 DB parameter group\.

## Deprecated versions for Amazon RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.DeprecatedVersions"></a>

RDS for PostgreSQL 9\.5 is deprecated as of March, 2021\. For more information about RDS for PostgreSQL 9\.5 deprecation, see [ Upgrading from Amazon RDS for PostgreSQL version 9\.5](http://aws.amazon.com/blogs/database/upgrading-from-amazon-rds-for-postgresql-version-9-5/)\.

To learn more about deprecation policy for RDS for PostgreSQL, see [Amazon RDS FAQs](http://aws.amazon.com/rds/faqs/)\. For more information about PostgreSQL versions, see [Versioning Policy](https://www.postgresql.org/support/versioning/) in the PostgreSQL documentation\.

## PostgreSQL extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions"></a>

RDS for PostgreSQL supports many PostgreSQL extensions\. The PostgreSQL community sometimes refers to these as modules\. Extensions expand on the functionality provided by the PostgreSQL engine\. You can find a list of extensions supported by Amazon RDS in the default DB parameter group for that PostgreSQL version\. You can also see the current extensions list using `psql` by showing the `rds.extensions` parameter as in the following example\.

```
SHOW rds.extensions; 
```

**Note**  
Parameters added in a minor version release might display inaccurately when using the `rds.extensions` parameter in `psql`\. 

The following sections show the extensions supported by Amazon RDS for the major PostgreSQL versions\.

**Contents**
+ [Restricting installation of PostgreSQL extensions](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.Restriction)
+ [PostgreSQL trusted extensions](#PostgreSQL.Concepts.General.Extensions.Trusted)
+ [PostgreSQL version 14 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.14x)
+ [PostgreSQL version 13 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x)
+ [PostgreSQL version 12 extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x)
+ [PostgreSQL version 11\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x)
+ [PostgreSQL version 10\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x)
+ [PostgreSQL version 9\.6\.x extensions supported on Amazon RDS](#PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x)

### Restricting installation of PostgreSQL extensions<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.Restriction"></a>

You can restrict which extensions can be installed on a PostgreSQL DB instance\. To do so, set the `rds.allowed_extensions` parameter to a string of comma\-separated extension names\. Only these extensions can then be installed in the PostgreSQL DB instance\.

The default string for the `rds.allowed_extensions` parameter is '\*', which means that any extension available for the engine version can be installed\. Changing the `rds.allowed_extensions` parameter does not require a database restart because it's a dynamic parameter\.

The PostgreSQL DB instance engine must be one of the following versions for you to use the `rds.allowed_extensions` parameter:
+ PostgreSQL 14\.1 or a higher minor version
+ PostgreSQL 13\.2 or a higher minor version
+ PostgreSQL 12\.6 or a higher minor version

 To see which extension installations are allowed, use the following psql command\.

```
postgres=> SHOW rds.allowed_extensions;
 rds.allowed_extensions
------------------------
 *
```

If an extension was installed prior to it being left out of the list in the `rds.allowed_extensions` parameter, the extension can still be used normally, and commands such as `ALTER EXTENSION` and `DROP EXTENSION` will continue to work\. However, after an extension is restricted, `CREATE EXTENSION` commands for the restricted extension will fail\.

Installation of extension dependencies with `CREATE EXTENSION CASCADE` are also restricted\. The extension and its dependencies must be specified in `rds.allowed_extensions`\. If an extension dependency installation fails, the entire `CREATE EXTENSION CASCADE` statement will fail\. 

If an extension is not included with the `rds.allowed_extensions` parameter, you will see an error such as the following if you try to install it\.

```
ERROR: permission denied to create extension "extension-name" 
HINT: This extension is not specified in "rds.allowed_extensions".
```

### PostgreSQL trusted extensions<a name="PostgreSQL.Concepts.General.Extensions.Trusted"></a>

To install most PostgreSQL extensions requires `rds_superuser` privileges\. PostgreSQL 13 introduced trusted extensions, which reduce the need to grant `rds_superuser` privileges to regular users\. With this feature, users can install many extensions if they have the `CREATE` privilege on the current database instead of requiring the `rds_superuser` role\. For more information, see the SQL [CREATE EXTENSION](https://www.postgresql.org/docs/current/sql-createextension.html) command in the PostgreSQL documentation\. 

The following lists the extensions that can be installed by a user who has the `CREATE` privilege on the current database and do not require the `rds_superuser` role:
+ bool\_plperl
+ [btree\_gin](http://www.postgresql.org/docs/current/btree-gin.html)
+ [btree\_gist](http://www.postgresql.org/docs/current/btree-gist.html)
+ [citext ](http://www.postgresql.org/docs/current/citext.html)
+ [cube ](http://www.postgresql.org/docs/current/cube.html)
+ [ dict\_int ](http://www.postgresql.org/docs/current/dict-int.html)
+ [fuzzystrmatch](http://www.postgresql.org/docs/current/fuzzystrmatch.html)
+  [hstore](http://www.postgresql.org/docs/current/hstore.html)
+ [ intarray](http://www.postgresql.org/docs/current/intarray.html)
+ [isn](http://www.postgresql.org/docs/current/isn.html)
+ jsonb\_plperl
+ [ltree ](http://www.postgresql.org/docs/current/ltree.html)
+ [pg\_trgm](http://www.postgresql.org/docs/current/pgtrgm.html)
+ [pgcrypto](http://www.postgresql.org/docs/current/pgcrypto.html)
+ [plperl](https://www.postgresql.org/docs/current/plperl.html)
+ [plpgsql](https://www.postgresql.org/docs/current/plpgsql.html)
+ [pltcl](https://www.postgresql.org/docs/current/pltcl-overview.html)
+ [tablefunc](http://www.postgresql.org/docs/current/tablefunc.html) 
+ [tsm\_system\_rows](https://www.postgresql.org/docs/current/tsm-system-rows.html)
+ [tsm\_system\_time](https://www.postgresql.org/docs/current/tsm-system-time.html)
+ [unaccent](http://www.postgresql.org/docs/current/unaccent.html)
+ [uuid\-ossp](http://www.postgresql.org/docs/current/uuid-ossp.html)

### PostgreSQL version 14 extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.14x"></a>

The following table shows PostgreSQL extensions for PostgreSQL version 14 that are currently supported on Amazon RDS\. For more information on PostgreSQL extensions, see [Packaging related objects into an extension](https://www.postgresql.org/docs/14/extend-extensions.html)\. 


| Extension | 14\.1 | 
| --- | --- | 
| [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 
| [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 
| [amcheck](https://www.postgresql.org/docs/14/amcheck.html) | 1\.3 | 
| [autoinc \(contrib\-spi\)](https://www.postgresql.org/docs/14/contrib-spi.html) | 1\.0 | 
| [auto\_explain](https://www.postgresql.org/docs/14/auto-explain.html) | yes | 
| [aws\_commons](USER_PostgreSQL.S3Import.md#USER_PostgreSQL.S3Import.Reference) | 1\.2 | 
| [aws\_lambda](PostgreSQL-Lambda.md) | 1\.0 | 
|  [aws\_s3\.table\_import\_from\_s3](USER_PostgreSQL.S3Import.md#aws_s3.table_import_from_s3) [aws\_s3\.query\_export\_to\_s3](postgresql-s3-export.md#aws_s3.export_query_to_s3)  | 1\.1 | 
| [bloom](https://www.postgresql.org/docs/14/bloom.html) | 1\.0 | 
| bool\_plperl | 1\.0 | 
| [btree\_gin](http://www.postgresql.org/docs/14/btree-gin.html) | 1\.3 | 
| [btree\_gist](http://www.postgresql.org/docs/14/btree-gist.html) | 1\.6 | 
| [citext](http://www.postgresql.org/docs/14/citext.html) | 1\.6 | 
| [cube](http://www.postgresql.org/docs/14/cube.html) | 1\.5 | 
| [dblink](http://www.postgresql.org/docs/14/dblink.html) | 1\.2 | 
| [dict\_int](http://www.postgresql.org/docs/14/dict-int.html) | 1\.0 | 
| [dict\_xsyn](https://www.postgresql.org/docs/14/dict-xsyn.html) | 1\.0 | 
| [earthdistance](http://www.postgresql.org/docs/14/earthdistance.html) | 1\.1 | 
| flow\_control | 1\.0 | 
| [fuzzystrmatch](http://www.postgresql.org/docs/14/fuzzystrmatch.html) | 1\.1 | 
| [hll](https://github.com/citusdata/postgresql-hll) | 2\.15 | 
| [hstore](http://www.postgresql.org/docs/14/hstore.html) | 1\.8 | 
| [hstore\_plperl](https://www.postgresql.org/docs/14/hstore.html) | 1\.0 | 
| [ICU module](http://site.icu-project.org/) | 60\.2 | 
| [insert\_username \(contrib\-spi\)](https://www.postgresql.org/docs/14/contrib-spi.html) | 1\.0 | 
| [intagg](http://www.postgresql.org/docs/14/intagg.html) | 1\.1 | 
| [intarray](http://www.postgresql.org/docs/14/intarray.html) | 1\.5 | 
| [ip4r](https://github.com/RhodiumToad/ip4r) | 2\.4 | 
| [isn](http://www.postgresql.org/docs/14/isn.html) | 1\.2 | 
| jsonb\_plperl | 1\.0 | 
| [log\_fdw](#CHAP_PostgreSQL.Extensions.log_fdw) | 1\.3 | 
| [ltree](http://www.postgresql.org/docs/14/ltree.html) | 1\.2 | 
| [moddatetime \(contrib\-spi\)](https://www.postgresql.org/docs/14/moddatetime.html) | 1\.0 | 
| [old\_snapshot](https://www.postgresql.org/docs/14/oldsnapshot.html) | 1\.0 | 
| [oracle\_fdw](https://github.com/laurenz/oracle_fdw) | 1\.2 | 
| [orafce](https://github.com/orafce/orafce) | 3\.15 | 
| [pageinspect](https://www.postgresql.org/docs/current/pageinspect.html) | 1\.9 | 
| [pg\_bigm](https://pgbigm.osdn.jp/index_en.html)  | 1\.2 | 
| [pg\_buffercache](http://www.postgresql.org/docs/current/pgbuffercache.html) | 1\.3 | 
| [pg\_cron](PostgreSQL_pg_cron.md) | 1\.4 | 
| [pg\_freespacemap](https://www.postgresql.org/docs/14/pgfreespacemap.html) | 1\.2 | 
| [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan) | 1\.3\.7 | 
| [pg\_partman](PostgreSQL_Partitions.md) | 4\.6\.0 | 
| [pg\_prewarm](https://www.postgresql.org/docs/14/pgprewarm.html) | 1\.2 | 
| [pg\_proctab](https://github.com/markwkm/pg_proctab) | 0\.0\.9 | 
| [ pg\_repack ](http://reorg.github.io/pg_repack/) | 1\.4\.7 | 
| [pg\_similarity](https://github.com/eulerto/pg_similarity) | 1\.0 | 
| [pg\_stat\_statements](http://www.postgresql.org/docs/14/pgstatstatements.html) | 1\.9 | 
| [pg\_transport](PostgreSQL.TransportableDB.md) | 1\.0 | 
| [pg\_trgm](http://www.postgresql.org/docs/14/pgtrgm.html) | 1\.6 | 
| [pg\_visibility](https://www.postgresql.org/docs/14/pgvisibility.html) | 1\.2 | 
| [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) | 1\.6 | 
| [pgcrypto](http://www.postgresql.org/docs/14/pgcrypto.html) | 1\.3 | 
| [pglogical](https://github.com/2ndQuadrant/pglogical) | 2\.4\.0 | 
| [pgrouting](http://docs.pgrouting.org/latest/en/index.html) | 3\.2\.0 | 
| [pgrowlocks](http://www.postgresql.org/docs/14/pgrowlocks.html) | 1\.2 | 
| [pgstattuple](http://www.postgresql.org/docs/14/pgstattuple.html) | 1\.5 | 
| [pgTAP](https://pgtap.org/)  | 1\.1\.0 | 
| plcoffee | 2\.3\.15 | 
| plls | 2\.3\.15 | 
| [plperl](https://www.postgresql.org/docs/14/plperl.html) | 1\.0 | 
| [plpgsql](https://www.postgresql.org/docs/14/plpgsql.html) | 1\.0 | 
| [plprofiler](https://github.com/bigsql/plprofiler) | 4\.1 | 
| [pltcl](https://www.postgresql.org/docs/14/pltcl-overview.html) | 1\.0 | 
| [plv8](#PostgreSQL.Concepts.General.UpgradingPLv8) | 2\.3\.15 | 
| [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md) | 3\.1\.4 | 
| [postgis\_raster](https://postgis.net/docs/raster.html) | 3\.1\.4 | 
| [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html) | 3\.1\.4 | 
| [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html) | 3\.1\.4 | 
| [postgres\_fdw](http://www.postgresql.org/docs/14/postgres-fdw.html) | 1\.1 | 
| [prefix](https://github.com/dimitri/prefix) | 1\.2\.0 | 
| [rdkit](https://github.com/rdkit/rdkit) | 3\.8 | 
| [rds\_tools](https://aws.amazon.com/blogs/database/scram-authentication-in-rds-for-postgresql-13) | 1\.0 | 
| [refint \(contrib\-spi\)](https://www.postgresql.org/docs/14/contrib-spi.html) | 1\.0 | 
| [sslinfo](http://www.postgresql.org/docs/14/sslinfo.html) | 1\.2 | 
| [tablefunc](http://www.postgresql.org/docs/14/tablefunc.html) | 1\.0 | 
| [test\_parser](https://www.postgresql.org/docs/9.4/test-parser.html) | 1\.0 | 
| [tsm\_system\_rows](https://www.postgresql.org/docs/14/tsm-system-rows.html) | 1\.0 | 
| [tsm\_system\_time](https://www.postgresql.org/docs/14/tsm-system-time.html) | 1\.0 | 
| [unaccent](http://www.postgresql.org/docs/14/unaccent.html) | 1\.1 | 
| [uuid\-ossp](http://www.postgresql.org/docs/14/uuid-ossp.html) | 1\.1 | 
| [wal2json](https://github.com/eulerto/wal2json) | 2\.3 | 

### PostgreSQL version 13 extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.13x"></a>

The following table shows PostgreSQL extensions for PostgreSQL version 13 that are currently supported on Amazon RDS\. For more information on PostgreSQL extensions, see [Packaging related objects into an extension](https://www.postgresql.org/docs/13/extend-extensions.html)\. 


| Extension | 13\.5 | 13\.4 | 13\.3 | 13\.2 | 13\.1 | 
| --- | --- | --- | --- | --- | --- | 
| [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.2 | 
| [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.2 | 
| [amcheck](https://www.postgresql.org/docs/current/amcheck.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| auto\_explain | yes | yes | yes | yes | yes | 
| [autoinc \(contrib\-spi\)](https://www.postgresql.org/docs/13/contrib-spi.html) | 1\.0 | 1\.0 | N/A | N/A | N/A | 
| [aws\_commons](USER_PostgreSQL.S3Import.md#USER_PostgreSQL.S3Import.Reference) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [aws\_lambda](PostgreSQL-Lambda.md) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | 
|  [aws\_s3\.table\_import\_from\_s3](USER_PostgreSQL.S3Import.md#aws_s3.table_import_from_s3) [aws\_s3\.query\_export\_to\_s3](postgresql-s3-export.md#aws_s3.export_query_to_s3)  | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [bloom](https://www.postgresql.org/docs/current/bloom.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| bool\_plperl | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [btree\_gin](http://www.postgresql.org/docs/current/btree-gin.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [btree\_gist](http://www.postgresql.org/docs/current/btree-gist.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [citext](http://www.postgresql.org/docs/current/citext.html) | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 
| [cube](http://www.postgresql.org/docs/current/cube.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [dblink](http://www.postgresql.org/docs/current/dblink.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [dict\_int](http://www.postgresql.org/docs/current/dict-int.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [dict\_xsyn](https://www.postgresql.org/docs/current/dict-xsyn.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [earthdistance](http://www.postgresql.org/docs/current/earthdistance.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [fuzzystrmatch](http://www.postgresql.org/docs/current/fuzzystrmatch.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [hll](https://github.com/citusdata/postgresql-hll) | 2\.15 | 2\.15 | 2\.15 | 2\.15 | 2\.15 | 
| [hstore](http://www.postgresql.org/docs/current/hstore.html) | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 
| [hstore\_plperl](https://www.postgresql.org/docs/current/hstore.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ICU module](http://site.icu-project.org/) | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 
| [insert\_username \(contrib\-spi\)](https://www.postgresql.org/docs/13/contrib-spi.html) | 1\.0 | 1\.0 | N/A | N/A | N/A | 
| [intagg](http://www.postgresql.org/docs/current/intagg.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [intarray](http://www.postgresql.org/docs/current/intarray.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [ip4r](https://github.com/RhodiumToad/ip4r) | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 
| [isn](http://www.postgresql.org/docs/current/isn.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| jsonb\_plperl | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [log\_fdw](#CHAP_PostgreSQL.Extensions.log_fdw) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [ltree](http://www.postgresql.org/docs/current/ltree.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [moddatetime \(contrib\-spi\)](https://www.postgresql.org/docs/13/contrib-spi.html) | 1\.0 | 1\.0 | N/A | N/A | N/A | 
| [oracle\_fdw](https://github.com/laurenz/oracle_fdw) | 2\.3\.0 | 2\.3\.0 | 2\.3\.0 | N/A | N/A | 
| [orafce](https://github.com/orafce/orafce) | 3\.15 | 3\.15 | 3\.15 | 3\.13\.4 | 3\.13\.4 | 
| [pageinspect](https://www.postgresql.org/docs/current/pageinspect.html) | 1\.8 | 1\.8 | 1\.8 | 1\.8 | 1\.8 | 
| [pg\_bigm](https://pgbigm.osdn.jp/index_en.html)  | 1\.2 | 1\.2 | 1\.2 | 1\.2 | N/A | 
| [pg\_buffercache](http://www.postgresql.org/docs/current/pgbuffercache.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pg\_cron](PostgreSQL_pg_cron.md) | 1\.4\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.0 | 1\.3\.0 | 
| [pg\_freespacemap](https://www.postgresql.org/docs/12/pgfreespacemap.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan) | 1\.3\.7 | 1\.3\.7 | 1\.3\.7 | 1\.3\.7 | 1\.3\.7 | 
| [pg\_partman](PostgreSQL_Partitions.md) | 4\.5\.1 | 4\.5\.1 | 4\.5\.1 | 4\.4\.0 | 4\.4\.0 | 
| [pg\_prewarm](https://www.postgresql.org/docs/current/pgprewarm.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_proctab](https://github.com/markwkm/pg_proctab) | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 
| [ pg\_repack ](http://reorg.github.io/pg_repack/) | 1\.4\.6 | 1\.4\.6 | 1\.4\.6 | 1\.4\.6 | 1\.4\.6 | 
| [pg\_similarity](https://github.com/eulerto/pg_similarity) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [pg\_stat\_statements](http://www.postgresql.org/docs/current/pgstatstatements.html) | 1\.8 | 1\.8 | 1\.8 | 1\.8 | 1\.8 | 
| [pg\_transport](PostgreSQL.TransportableDB.md) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [pg\_trgm](http://www.postgresql.org/docs/current/pgtrgm.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [pg\_visibility](https://www.postgresql.org/docs/current/pgvisibility.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [pgcrypto](http://www.postgresql.org/docs/current/pgcrypto.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pglogical](https://github.com/2ndQuadrant/pglogical) | 2\.4\.0 | 2\.4\.0 | 2\.3\.3 | 2\.3\.3 | 2\.3\.3 | 
| [pgrouting](http://docs.pgrouting.org/latest/en/index.html) | 3\.1\.3 | 3\.1\.3 | 3\.1\.0 | 3\.1\.0 | 3\.1\.0 | 
| [pgrowlocks](http://www.postgresql.org/docs/current/pgrowlocks.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgstattuple](http://www.postgresql.org/docs/current/pgstattuple.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [pgTAP](https://pgtap.org/)  | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 
| plcoffee | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 
| plls | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 
| [plperl](https://www.postgresql.org/docs/current/plperl.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plpgsql](https://www.postgresql.org/docs/current/plpgsql.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plprofiler](https://github.com/bigsql/plprofiler) | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 
| [pltcl](https://www.postgresql.org/docs/current/pltcl-overview.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plv8](#PostgreSQL.Concepts.General.UpgradingPLv8) | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 2\.3\.15 | 
| [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.2 | 
| [postgis\_raster](https://postgis.net/docs/raster.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.2 | 
| [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.2 | 
| [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.2 | 
| [postgres\_fdw](http://www.postgresql.org/docs/current/postgres-fdw.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [prefix](https://github.com/dimitri/prefix) | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 
| [rdkit](https://github.com/rdkit/rdkit) | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 
| [rds\_tools](https://aws.amazon.com/blogs/database/scram-authentication-in-rds-for-postgresql-13) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [refint \(contrib\-spi\)](https://www.postgresql.org/docs/13/contrib-spi.html) | 1\.0 | 1\.0 | N/A | N/A | N/A | 
| [sslinfo](http://www.postgresql.org/docs/current/sslinfo.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [tablefunc](http://www.postgresql.org/docs/current/tablefunc.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [test\_parser](https://www.postgresql.org/docs/9.4/test-parser.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsm\_system\_rows](https://www.postgresql.org/docs/current/tsm-system-rows.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsm\_system\_time](https://www.postgresql.org/docs/current/tsm-system-time.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [unaccent](http://www.postgresql.org/docs/current/unaccent.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [uuid\-ossp](http://www.postgresql.org/docs/current/uuid-ossp.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [wal2json](https://github.com/eulerto/wal2json) | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 

### PostgreSQL version 12 extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.12x"></a>

The following table shows PostgreSQL extensions for PostgreSQL version 12 that are currently supported on Amazon RDS\. For more information on PostgreSQL extensions, see [Packaging related objects into an extension](https://www.postgresql.org/docs/12/extend-extensions.html)\. 


| Extension | 12\.9 | 12\.8 | 12\.7 | 12\.6 | 12\.5 | 12\.4 | 12\.3 | 12\.2 | 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [amcheck](https://www.postgresql.org/docs/current/amcheck.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| auto\_explain | yes | yes | yes | yes | yes | yes | yes | yes | 
| [aws\_commons](USER_PostgreSQL.S3Import.md#USER_PostgreSQL.S3Import.Reference) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [aws\_lambda](PostgreSQL-Lambda.md) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | N/A | N/A | N/A | 
|  [aws\_s3\.table\_import\_from\_s3](USER_PostgreSQL.S3Import.md#aws_s3.table_import_from_s3) [aws\_s3\.query\_export\_to\_s3](postgresql-s3-export.md#aws_s3.export_query_to_s3)  | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.0 | 1\.0 | 
| [bloom](https://www.postgresql.org/docs/12/bloom.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [btree\_gin](http://www.postgresql.org/docs/12/btree-gin.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [btree\_gist](http://www.postgresql.org/docs/12/btree-gist.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [citext](http://www.postgresql.org/docs/12/citext.html) | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 
| [cube](http://www.postgresql.org/docs/12/cube.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [dblink](http://www.postgresql.org/docs/12/dblink.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [dict\_int](http://www.postgresql.org/docs/12/dict-int.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [dict\_xsyn](https://www.postgresql.org/docs/12/dict-xsyn.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [earthdistance](http://www.postgresql.org/docs/12/earthdistance.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [fuzzystrmatch](http://www.postgresql.org/docs/12/fuzzystrmatch.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [hll](https://github.com/citusdata/postgresql-hll) | 2\.14 | 2\.14 | 2\.14 | 2\.14 | 2\.14 | 2\.14 | 2\.14 | 2\.14 | 
| [hstore](http://www.postgresql.org/docs/12/hstore.html) | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 
| [hstore\_plperl](https://www.postgresql.org/docs/12/hstore.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ICU module](http://site.icu-project.org/) | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 
| [intagg](http://www.postgresql.org/docs/12/intagg.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [intarray](http://www.postgresql.org/docs/12/intarray.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [ip4r](https://github.com/RhodiumToad/ip4r) | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 2\.4 | 
| [isn](http://www.postgresql.org/docs/12/isn.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| jsonb\_plperl | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [log\_fdw](#CHAP_PostgreSQL.Extensions.log_fdw) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [ltree](http://www.postgresql.org/docs/12/ltree.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [oracle\_fdw](https://github.com/laurenz/oracle_fdw) | 2\.3\.0 | 2\.3\.0 | 2\.3\.0 | N/A | N/A | N/A | N/A | N/A | 
| [orafce](https://github.com/orafce/orafce) | 3\.15 | 3\.15 | 3\.15 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 
| [pageinspect](https://www.postgresql.org/docs/current/pageinspect.html) | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 
| [pg\_bigm](https://pgbigm.osdn.jp/index_en.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | N/A | N/A | N/A | N/A | 
| [pg\_buffercache](http://www.postgresql.org/docs/12/pgbuffercache.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pg\_cron](PostgreSQL_pg_cron.md) | 1\.4\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.0 | 1\.3\.0 | N/A | N/A | N/A | 
| [pg\_freespacemap](https://www.postgresql.org/docs/12/pgfreespacemap.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan) | 1\.3\.7 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.4 | 
| [pg\_partman](PostgreSQL_Partitions.md) | 4\.5\.1 | 4\.5\.1 | 4\.5\.1 | 4\.4\.0 | 4\.4\.0 | N/A | N/A | N/A | 
| [pg\_prewarm](https://www.postgresql.org/docs/12/pgprewarm.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_proctab](https://github.com/markwkm/pg_proctab) | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | N/A | N/A | 
| [pg\_repack](http://reorg.github.io/pg_repack/) | 1\.4\.5 | 1\.4\.5 | 1\.4\.5 | 1\.4\.5 | 1\.4\.5 | 1\.4\.5 | 1\.4\.5 | 1\.4\.5 | 
| [pg\_similarity](https://github.com/eulerto/pg_similarity) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [pg\_stat\_statements](http://www.postgresql.org/docs/12/pgstatstatements.html) | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 1\.7 | 
| [pg\_transport](PostgreSQL.TransportableDB.md) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [pg\_trgm](http://www.postgresql.org/docs/12/pgtrgm.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [pg\_visibility](https://www.postgresql.org/docs/12/pgvisibility.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [pgcrypto](http://www.postgresql.org/docs/12/pgcrypto.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pglogical](https://github.com/2ndQuadrant/pglogical) | 2\.4\.0 | 2\.4\.0 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.1 | 2\.3\.0 | 
| [pgrouting](http://docs.pgrouting.org/2.3/en/doc/index.html) | 3\.0\.5 | 3\.0\.5 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [pgrowlocks](http://www.postgresql.org/docs/12/pgrowlocks.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgstattuple](http://www.postgresql.org/docs/12/pgstattuple.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [pgTAP](https://pgtap.org/)  | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 
| plcoffee | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 
| plls | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 
| [plperl](https://www.postgresql.org/docs/12/plperl.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plpgsql](https://www.postgresql.org/docs/12/plpgsql.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plprofiler](https://github.com/bigsql/plprofiler) | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 
| [pltcl](https://www.postgresql.org/docs/12/pltcl-overview.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plv8](#PostgreSQL.Concepts.General.UpgradingPLv8) | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 2\.3\.14 | 
| [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [postgis\_raster](https://postgis.net/docs/raster.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html) | 3\.1\.4 | 3\.1\.4 | 3\.0\.3 | 3\.0\.2 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 3\.0\.0 | 
| [postgres\_fdw](http://www.postgresql.org/docs/12/postgres-fdw.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [prefix](https://github.com/dimitri/prefix) | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 
| [rdkit](https://github.com/rdkit/rdkit) | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | N/A | N/A | 
| [sslinfo](http://www.postgresql.org/docs/12/sslinfo.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [tablefunc](http://www.postgresql.org/docs/12/tablefunc.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [test\_parser](https://www.postgresql.org/docs/9.4/static/test-parser.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsm\_system\_rows](https://www.postgresql.org/docs/12/tsm-system-rows.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsm\_system\_time](https://www.postgresql.org/docs/12/tsm-system-time.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [unaccent](http://www.postgresql.org/docs/12/unaccent.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [uuid\-ossp](http://www.postgresql.org/docs/12/uuid-ossp.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [wal2json](https://github.com/eulerto/wal2json) | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.1 | 2\.1 | 

### PostgreSQL version 11\.x extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.11x"></a>

The following tables show PostgreSQL extensions for PostgreSQL version 11\.x that are currently supported by RDS for PostgreSQL\. "N/A" indicates that the extension is not available for that PostgreSQL version\. For more information on PostgreSQL extensions, see [Packaging related objects into an extension](https://www.postgresql.org/docs/11/extend-extensions.html)\. 


| Extension | 11\.14 | 11\.13 | 11\.12 | 11\.11 | 11\.10 | 11\.9 | 11\.8 | 11\.7 | 11\.6 | 11\.5 | 11\.4 | 11\.2 | 11\.1 | 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 
| [address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 
|  [aws\_s3\.table\_import\_from\_s3](USER_PostgreSQL.S3Import.md#aws_s3.table_import_from_s3) [aws\_s3\.query\_export\_to\_s3](postgresql-s3-export.md#aws_s3.export_query_to_s3)  | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [amcheck](https://www.postgresql.org/docs/current/amcheck.html) | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| auto\_explain | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [bloom](https://www.postgresql.org/docs/11/static/bloom.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [btree\_gin](http://www.postgresql.org/docs/11/static/btree-gin.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [btree\_gist](http://www.postgresql.org/docs/11/static/btree-gist.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [citext](http://www.postgresql.org/docs/11/static/citext.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [cube](http://www.postgresql.org/docs/11/static/cube.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [dblink](http://www.postgresql.org/docs/11/static/dblink.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| decoder\_raw | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [dict\_int](http://www.postgresql.org/docs/11/static/dict-int.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [dict\_xsyn](https://www.postgresql.org/docs/11/static/dict-xsyn.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [earthdistance](http://www.postgresql.org/docs/11/static/earthdistance.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [fuzzystrmatch](http://www.postgresql.org/docs/11/static/fuzzystrmatch.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [hstore](http://www.postgresql.org/docs/11/static/hstore.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [hstore\_plperl](https://www.postgresql.org/docs/11/static/hstore.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ICU module](http://site.icu-project.org/) | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 60\.2  | 
| [intagg](http://www.postgresql.org/docs/11/static/intagg.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [intarray](http://www.postgresql.org/docs/11/static/intarray.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [ip4r](https://github.com/RhodiumToad/ip4r) | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 
| [isn ](http://www.postgresql.org/docs/11/static/isn.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [log\_fdw](#CHAP_PostgreSQL.Extensions.log_fdw) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| libprotobuf | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 
| [ltree ](http://www.postgresql.org/docs/11/static/ltree.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [orafce](https://github.com/orafce/orafce) | 3\.15 | 3\.15 | 3\.15 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.7 | 3\.7 | 3\.7 | 3\.7 | 3\.7 | 
| pageinspect | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 
| [pg\_bigm](https://pgbigm.osdn.jp/index_en.html)  | 1\.2 | 1\.2 | 1\.2 | 1\.2 | NA | NA | NA | NA | NA | NA | NA | NA | NA | 
| [pg\_buffercache](http://www.postgresql.org/docs/11/static/pgbuffercache.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pg\_freespacemap](https://www.postgresql.org/docs/11/static/pgfreespacemap.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan) | 1\.3\.7 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.4 | 1\.3\.4 | 1\.3\.4 | 1\.3\.4 | 1\.3\.2 | 1\.3\.2 | 
| [pg\_prewarm](https://www.postgresql.org/docs/11/static/pgprewarm.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_proctab](https://github.com/markwkm/pg_proctab) | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | 0\.0\.9 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [pg\_repack](http://reorg.github.io/pg_repack/) | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 1\.4\.4 | 
| pg\_similarity | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [pg\_stat\_statements](http://www.postgresql.org/docs/11/static/pgstatstatements.html) | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 
| pg\_transport | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | N/A | N/A | 
| [pg\_trgm](http://www.postgresql.org/docs/11/static/pgtrgm.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [pg\_visibility](https://www.postgresql.org/docs/11/static/pgvisibility.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 
| [pgcrypto](http://www.postgresql.org/docs/11/static/pgcrypto.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pglogical](https://github.com/2ndQuadrant/pglogical) | 2\.4\.0 | 2\.4\.0 | 2\.2\.2 | 2\.2\.2 | 2\.2\.2 | 2\.2\.2 | 2\.2\.1 | 2\.2\.1 | 2\.2\.1 | 2\.2\.1 | 2\.2\.1 | 2\.2\.1 | 2\.2\.1 | 
| [pgrowlocks](http://www.postgresql.org/docs/11/static/pgrowlocks.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgrouting](http://docs.pgrouting.org/2.3/en/doc/index.html) | 2\.6\.3 | 2\.6\.3 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 2\.6\.1 | 
| [pgstattuple](http://www.postgresql.org/docs/11/static/pgstattuple.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
|  [pgTAP](https://pgtap.org/)  | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | 
| plcoffee | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 
| plls | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 
| [plperl](https://www.postgresql.org/docs/11/static/plperl.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plpgsql](https://www.postgresql.org/docs/11/static/plpgsql.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plprofiler](https://github.com/bigsql/plprofiler) | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | N/A | N/A | N/A | N/A | 
| [pltcl](https://www.postgresql.org/docs/11/static/pltcl-overview.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plv8](#PostgreSQL.Concepts.General.UpgradingPLv8) | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 2\.3\.8 | 
| [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md) | 3\.1\.4 | 3\.1\.4 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 
| [postgis\_raster](https://postgis.net/docs/raster.html) | 3\.1\.4 | 3\.1\.4 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html) | 3\.1\.4 | 3\.1\.4 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 
| [postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html) | 3\.1\.4 | 3\.1\.4 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 2\.5\.1 | 
| [postgres\_fdw](http://www.postgresql.org/docs/11/static/postgres-fdw.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [postgresql\-hll](https://github.com/citusdata/postgresql-hll/releases/tag/v2.10.2) | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 2\.11 | 
|  [prefix](https://github.com/dimitri/prefix) | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 1\.2\.8 | 
| [rdkit](https://github.com/rdkit/rdkit) | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [sslinfo](http://www.postgresql.org/docs/11/static/sslinfo.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [tablefunc](http://www.postgresql.org/docs/11/static/tablefunc.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| test\_decoding | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [test\_parser](https://www.postgresql.org/docs/9.4/static/test-parser.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsm\_system\_rows](https://www.postgresql.org/docs/11/static/tsm-system-rows.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsm\_system\_time](https://www.postgresql.org/docs/11/static/tsm-system-time.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
|  [unaccent](http://www.postgresql.org/docs/11/static/unaccent.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [uuid\-ossp](http://www.postgresql.org/docs/11/static/uuid-ossp.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [wal2json](https://github.com/eulerto/wal2json) | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.1 | 2\.1 | Commit hash 9e962bad | Commit hash 9e962bad | Commit hash 9e962bad | Commit hash 9e962bad | Commit hash 9e962bad | 

### PostgreSQL version 10\.x extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.101x"></a>

The following tables show PostgreSQL extensions for PostgreSQL version 10 that are currently supported by RDS for PostgreSQL\. "N/A" indicates that the extension is not available for that PostgreSQL version\. For more information on PostgreSQL extensions, see [Packaging related objects into an extension](https://www.postgresql.org/docs/10/extend-extensions.html)\. 


| Extension | 10\.19 | 10\.18 | 10\.17 | 10\.16 | 10\.15 | 10\.14 | 10\.13 | 10\.12 | 10\.11 | 10\.10 | 10\.9 | 10\.7 | 10\.6 | 10\.5 | 10\.4 | 10\.3 | 10\.1 | 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| [address\_standardizer](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 
| [ address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html) | 3\.1\.4 | 3\.1\.4 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 
| amcheck | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | N/A | 
| auto\_explain | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [aws\_s3](USER_PostgreSQL.S3Import.md)  | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [ bloom](https://www.postgresql.org/docs/10/static/bloom.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [btree\_gin](http://www.postgresql.org/docs/10/static/btree-gin.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [btree\_gist](http://www.postgresql.org/docs/10/static/btree-gist.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| [chkpass](http://www.postgresql.org/docs/10/static/chkpass.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [citext](http://www.postgresql.org/docs/10/static/citext.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [cube](http://www.postgresql.org/docs/10/static/cube.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [dblink](http://www.postgresql.org/docs/10/static/dblink.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| decoder\_raw | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [dict\_int](http://www.postgresql.org/docs/10/static/dict-int.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [dict\_xsyn](https://www.postgresql.org/docs/10/static/dict-xsyn.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [earthdistance](http://www.postgresql.org/docs/10/static/earthdistance.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [fuzzystrmatch](http://www.postgresql.org/docs/10/static/fuzzystrmatch.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [hstore](http://www.postgresql.org/docs/10/static/hstore.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [hstore\_plperl](https://www.postgresql.org/docs/10/static/hstore.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ICU module](http://site.icu-project.org/) | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 60\.2 | 
| [ intagg](http://www.postgresql.org/docs/10/static/intagg.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [ intarray](http://www.postgresql.org/docs/10/static/intarray.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [ip4r](https://github.com/RhodiumToad/ip4r) | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.0 | 2\.0 | 
| [isn](http://www.postgresql.org/docs/10/static/isn.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [log\_fdw](#CHAP_PostgreSQL.Extensions.log_fdw) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| libprotobuf | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | N/A | N/A | N/A | 
| [ltree](http://www.postgresql.org/docs/10/static/ltree.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [orafce](https://github.com/orafce/orafce) | 3\.15 | 3\.15 | 3\.15 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 
| [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) | 1\.2\.1 | 1\.2\.1 | 1\.2\.1 | 1\.2\.1 | 1\.2\.1 | 1\.2\.1 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 
| [pg\_buffercache](http://www.postgresql.org/docs/10/static/pgbuffercache.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pg\_freespacemap](https://www.postgresql.org/docs/10/static/pgfreespacemap.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan) | 1\.3\.6 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.5 | 1\.3\.3 | 1\.3\.3 | 1\.3\.3 | 1\.3\.3 | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.0 | 1\.3\.0 | 1\.3\.0 | 
| [pg\_prewarm](https://www.postgresql.org/docs/10/static/pgprewarm.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [pg\_repack ](http://reorg.github.io/pg_repack/) | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.2 | 1\.4\.2 | 
| pg\_similarity | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | N/A | N/A | 
| [pg\_stat\_statements](http://www.postgresql.org/docs/10/static/pgstatstatements.html) | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| pg\_transport | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [pg\_trgm](http://www.postgresql.org/docs/10/static/pgtrgm.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pg\_visibility](https://www.postgresql.org/docs/10/static/pgvisibility.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgcrypto](http://www.postgresql.org/docs/10/static/pgcrypto.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| pageinspect | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | 1\.6 | N/A | N/A | N/A | 
| [pglogical](https://github.com/2ndQuadrant/pglogical) | 2\.4\.0 | 2\.4\.0 | 2\.2\.2 | 2\.2\.2 | 2\.2\.2 | 2\.2\.2 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | N/A | N/A | N/A | 
| [pgrowlocks](http://www.postgresql.org/docs/10/static/pgrowlocks.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgrouting](http://docs.pgrouting.org/2.3/en/doc/index.html) | 2\.5\.5 | 2\.5\.5 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 
| [pgstattuple](http://www.postgresql.org/docs/10/static/pgstattuple.html) | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 1\.5 | 
| plcoffee | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.0 | 2\.1\.0 | 
| plls | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.0 | 2\.1\.0 | 
| [plperl](https://www.postgresql.org/docs/10/static/plperl.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plpgsql](https://www.postgresql.org/docs/10/static/plpgsql.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plprofiler](https://github.com/bigsql/plprofiler) | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | 4\.1 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [ pltcl](https://www.postgresql.org/docs/10/static/pltcl-overview.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plv8](#PostgreSQL.Concepts.General.UpgradingPLv8) | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.0 | 2\.1\.0 | 
| [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md) | 3\.1\.4 | 3\.1\.4 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.4\.4 | 2\.4\.4 | 2\.4\.4 | 2\.4\.4 | 2\.4\.4 | 2\.4\.2 | 2\.4\.2 | 
| [postgis\_raster](https://postgis.net/docs/raster.html) | 3\.1\.4 | 3\.1\.4 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [ postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html) | 3\.1\.4 | 3\.1\.4 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 
| [ postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html) | 3\.1\.4 | 3\.1\.4 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 
| [postgres\_fdw](http://www.postgresql.org/docs/10/static/postgres-fdw.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ postgresql\-hll](https://github.com/citusdata/postgresql-hll/releases/tag/v2.10.2) | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 
|  [ prefix](https://github.com/dimitri/prefix) | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 1\.2\.0 | 
| [sslinfo](http://www.postgresql.org/docs/10/static/sslinfo.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [tablefunc](http://www.postgresql.org/docs/10/static/tablefunc.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| test\_decoding | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [ test\_parser](https://www.postgresql.org/docs/9.4/static/test-parser.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsearch2](http://www.postgresql.org/docs/9.6/static/tsearch2.html) \(deprecated\) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ tsm\_system\_rows](https://www.postgresql.org/docs/10/static/tsm-system-rows.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ tsm\_system\_time](https://www.postgresql.org/docs/10/static/tsm-system-time.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
|  [unaccent ](http://www.postgresql.org/docs/10/static/unaccent.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [uuid\-ossp](http://www.postgresql.org/docs/10/static/uuid-ossp.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [wal2json](https://github.com/eulerto/wal2json) | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.3 | 2\.1 | 2\.1 | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 01c5c1e | Commit hash 5352cc4 | Commit hash 5352cc4 | Commit hash 5352cc4 | 

The `tsearch2` extension is deprecated in version 10\. The `tsearch2` extension was remove from [PostgreSQL version 11\.1 on Amazon RDS](#PostgreSQL.Concepts.General.version111)\.

### PostgreSQL version 9\.6\.x extensions supported on Amazon RDS<a name="PostgreSQL.Concepts.General.FeatureSupport.Extensions.96x"></a>

RDS for PostgreSQL 9\.6 will be deprecated on April 26, 2022\. For more information, see [Deprecation of PostgreSQL version 9\.6](#PostgreSQL.Concepts.General.DBVersions.Deprecation96)\. The information following is retained for historical purposes only\. 

The following tables show PostgreSQL extensions for PostgreSQL version 9\.6\.x that are currently supported by RDS for PostgreSQL\. "N/A" indicates that the extension is not available for that PostgreSQL version\. For more information on PostgreSQL extensions, see [Packaging related objects into an extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)\. 


| Extension | 9\.6\.24 | 9\.6\.23 | 9\.6\.22 | 9\.6\.20 | 9\.6\.19 | 9\.6\.18 | 9\.6\.17 | 9\.6\.16 | 9\.6\.15 | 9\.6\.14 | 9\.6\.12 | 9\.6\.11 | 9\.6\.10 | 9\.6\.9 | 9\.6\.8 | 9\.6\.6 | 9\.6\.5 | 9\.6\.3 | 9\.6\.2 | 9\.6\.1 | 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| [ address\_standardizer](http://postgis.net/docs/Address_Standardizer.html) | 2\.5\.5, 2\.3\.7 | 2\.5\.5, 2\.3\.7 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.0 | 
| [ address\_standardizer\_data\_us](http://postgis.net/docs/Address_Standardizer.html) | 2\.5\.5, 2\.3\.7 | 2\.5\.5, 2\.3\.7 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.0 | 
| auto\_explain | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | N/A | N/A | 
| [ bloom](https://www.postgresql.org/docs/9.6/static/bloom.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [btree\_gin](http://www.postgresql.org/docs/9.6/static/btree-gin.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [btree\_gist](http://www.postgresql.org/docs/9.6/static/btree-gist.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [chkpass](http://www.postgresql.org/docs/9.6/static/chkpass.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [citext ](http://www.postgresql.org/docs/9.6/static/citext.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [cube ](http://www.postgresql.org/docs/9.6/static/cube.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [ dblink](http://www.postgresql.org/docs/9.6/static/dblink.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| decoder\_raw | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | N/A | N/A | N/A | 
| [ dict\_int ](http://www.postgresql.org/docs/9.6/static/dict-int.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ dict\_xsyn](https://www.postgresql.org/docs/9.6/static/dict-xsyn.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [earthdistance](http://www.postgresql.org/docs/9.6/static/earthdistance.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [fuzzystrmatch](http://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [hstore](http://www.postgresql.org/docs/9.6/static/hstore.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [ hstore\_plperl](https://www.postgresql.org/docs/9.6/static/hstore.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ intagg](http://www.postgresql.org/docs/9.6/static/intagg.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [ intarray](http://www.postgresql.org/docs/9.6/static/intarray.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [ip4r](https://github.com/RhodiumToad/ip4r) | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.1\.1 | 2\.0 | 2\.0 | 2\.0 | 2\.0 | 2\.0 | 2\.0 | 
| [isn ](http://www.postgresql.org/docs/9.6/static/isn.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [log\_fdw](#CHAP_PostgreSQL.Extensions.log_fdw) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | 
| [ltree ](http://www.postgresql.org/docs/9.6/static/ltree.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [orafce](https://github.com/orafce/orafce) | 3\.15 | 3\.15 | 3\.15 | 3\.8 | 3\.8 | 3\.8 | 3\.8 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | 3\.6\.1 | N/A | N/A | N/A | N/A | 
| [pgaudit](https://github.com/pgaudit/pgaudit/blob/master/README.md) | 1\.1\.2 | 1\.1\.2 | 1\.1\.2 | 1\.1\.2 | 1\.1\.2 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | N/A | N/A | 
| [ pg\_buffercache](http://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pg\_freespacemap](https://www.postgresql.org/docs/current/static/pgfreespacemap.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | N/A | 
| [pg\_hint\_plan](https://github.com/ossc-db/pg_hint_plan) | 1\.2\.7 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.5 | 1\.2\.5 | 1\.2\.5 | 1\.2\.5 | 1\.2\.3 | 1\.2\.3 | 1\.2\.3 | 1\.2\.2 | 1\.2\.2 | 1\.1\.3 | 1\.1\.3 | 1\.1\.3 | 1\.1\.3 | N/A | 
| [ pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [ pg\_repack ](http://reorg.github.io/pg_repack/) | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.3 | 1\.4\.2 | 1\.4\.2 | 1\.4\.1 | 1\.4\.0 | N/A | N/A | 
| pg\_similarity | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [pg\_stat\_statements](http://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| [pg\_trgm](http://www.postgresql.org/docs/9.6/static/pgtrgm.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [ pg\_visibility](https://www.postgresql.org/docs/9.6/static/pgvisibility.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [pgcrypto](http://www.postgresql.org/docs/9.6/static/pgcrypto.html) | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 1\.3 | 
| [pglogical](https://github.com/2ndQuadrant/pglogical) | 2\.4\.0 | 2\.4\.0 | 2\.2\.2 | 2\.2\.2 | 2\.2\.2 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | N/A | N/A | N/A | N/A | N/A | N/A | N/A | 
| [pgrowlocks](http://www.postgresql.org/docs/9.6/static/pgrowlocks.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [pgrouting](http://docs.pgrouting.org/2.3/en/doc/index.html) | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.4\.2 | 2\.3\.2 | N/A | N/A | N/A | 
| [pgstattuple](http://www.postgresql.org/docs/9.6/static/pgstattuple.html) | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 1\.4 | 
| plcoffee | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 
| plls | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 
| [ plperl](https://www.postgresql.org/docs/current/static/plperl.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ plpgsql](https://www.postgresql.org/docs/current/static/plpgsql.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ pltcl](https://www.postgresql.org/docs/current/static/pltcl-overview.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [plv8](#PostgreSQL.Concepts.General.UpgradingPLv8) | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.2 | 2\.1\.0 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 1\.5\.3 | 
| [PostGIS](Appendix.PostgreSQL.CommonDBATasks.PostGIS.md) | 2\.5\.5, 2\.3\.7 | 2\.5\.5, 2\.3\.7 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.5\.2 | 2\.3\.7 | 2\.3\.7 | 2\.3\.7 | 2\.3\.7 | 2\.3\.7 | 2\.3\.4 | 2\.3\.4 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.0 | 
| [ postgis\_tiger\_geocoder](http://postgis.net/docs/Geocode.html) | 2\.5\.5, 2\.3\.7 | 2\.5\.5, 2\.3\.7 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.0 | 
| [ postgis\_topology](http://postgis.net/docs/manual-dev/Topology.html) | 2\.5\.5, 2\.3\.7 | 2\.5\.5, 2\.3\.7 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.4 | 2\.3\.2 | 2\.3\.2 | 2\.3\.2 | 2\.3\.0 | 
| [postgres\_fdw](http://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ postgresql\-hll](https://github.com/citusdata/postgresql-hll/releases/tag/v2.10.2) | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | 2\.10\.2 | N/A | N/A | N/A | 
|  [ prefix](https://github.com/dimitri/prefix) | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | 1\.2\.6 | N/A | N/A | N/A | N/A | 
| [sslinfo](http://www.postgresql.org/docs/9.6/static/sslinfo.html) | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 1\.2 | 
| [tablefunc](http://www.postgresql.org/docs/9.6/static/tablefunc.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| test\_decoding | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | 
| [ test\_parser](https://www.postgresql.org/docs/9.4/static/test-parser.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [tsearch2](http://www.postgresql.org/docs/9.6/static/tsearch2.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ tsm\_system\_rows](https://www.postgresql.org/docs/current/static/tsm-system-rows.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
| [ tsm\_system\_time](https://www.postgresql.org/docs/current/static/tsm-system-time.html) | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 1\.0 | 
|  [unaccent ](http://www.postgresql.org/docs/9.6/static/unaccent.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [uuid\-ossp](http://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 1\.1 | 
| [wal2json](https://github.com/eulerto/wal2json) | version 2\.3 | version 2\.3 | version 2\.3 | version 2\.3 | version 2\.3 | version 2\.1 | version 2\.1 | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 9e962ba | Commit hash 01c5c1e | Commit hash 5352cc4 | Commit hash 5352cc4 | Commit hash 645ab69 | Commit hash 645ab69 | Commit hash 2828409 | N/A | N/A | 

## PostgreSQL features supported by RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport"></a>

RDS for PostgreSQL supports many of the most common PostgreSQL extensions and features\.

**Topics**
+ [Using the log\_fdw extension](#CHAP_PostgreSQL.Extensions.log_fdw)
+ [Upgrading PLV8](#PostgreSQL.Concepts.General.UpgradingPLv8)
+ [Logical replication for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.LogicalReplication)
+ [Event triggers for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.EventTriggers)
+ [Huge pages for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.HugePages)
+ [Tablespaces for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.Tablespaces)
+ [Autovacuum for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.Autovacuum)
+ [RAM disk for the stats\_temp\_directory](#PostgreSQL.Concepts.General.FeatureSupport.RamDisk)
+ [ALTER ENUM for RDS for PostgreSQL](#PostgreSQL.Concepts.General.FeatureSupport.AlterEnum)

### Using the log\_fdw extension<a name="CHAP_PostgreSQL.Extensions.log_fdw"></a>

RDS for PostgreSQL supports the `log_fdw` extension which lets you access your database engine log using a SQL interface\. You can view the default *stderr* log files that are generated by Amazon RDS\. You can also view comma\-separated values \(CSV\) logs and build foreign tables with the data neatly split into several columns\. To do so, you first set the `log_destination` parameter to `csvlog` on your RDS for PostgreSQL DB instance, which means that you need to be using a custom DB parameter group for the instance\. To learn how, see [Working with RDS for PostgreSQL parameters](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.Parameters)\. 

The `log_fdw` extension provides two functions that make it easy to create foreign tables for database logs:
+ `list_postgres_log_files()` – Lists the files in the database log directory and the file size in bytes\.
+ `create_foreign_table_for_log_file(table_name text, server_name text, log_file_name text)` – Builds a foreign table for the specified file in the current database\.

All functions created by `log_fdw` are owned by `rds_superuser`\. Members of the `rds_superuser` role can grant access to these functions to other database users\.

The following example shows how to use the `log_fdw` extension with an RDS for PostgreSQL DB instance with the `log_destination` parameter set to `csvlog`\. 

**To use the log\_fdw extension**

1. Get the `log_fdw` extension\.

   ```
   postgres=> CREATE EXTENSION log_fdw;
   CREATE EXTENSION
   ```

1. Create the log server as a foreign data wrapper\.

   ```
   postgres=> CREATE SERVER log_server FOREIGN DATA WRAPPER log_fdw;
   CREATE SERVER
   ```

1. Select all from a list of log files\.

   ```
   postgres=> SELECT * from list_postgres_log_files() ORDER BY 1;
   ```

   A sample response is as follows\.

   ```
             file_name           | file_size_bytes
   ------------------------------+-----------------
    postgresql.log.2016-08-09-22.csv |            1111
    postgresql.log.2016-08-09-23.csv |            1172
    postgresql.log.2016-08-10-00.csv |            1744
    postgresql.log.2016-08-10-01.csv |            1102
   (4 rows)
   ```

1. Create a table with a single 'log\_entry' column for the selected file\.

   ```
   postgres=> SELECT create_foreign_table_for_log_file('my_postgres_error_log', 
        'log_server', 'postgresql.log.2016-08-09-22.csv');
   ```

   The response provides no detail other than that the table now exists\.

   ```
   -----------------------------------
   (1 row)
   ```

1. Select a sample of the log file\. The following code retrieves the log time and error message description\.

   ```
   postgres=> SELECT log_time, message from my_postgres_error_log ORDER BY 1;
   ```

   A sample response is as follows\.

   ```
                log_time             |                                  message                                 
   ----------------------------------+---------------------------------------------------------------------------
   Tue Aug 09 15:45:18.172 2016 PDT | ending log output to stderr
   Tue Aug 09 15:45:18.175 2016 PDT | database system was interrupted; last known up at 2016-08-09 22:43:34 UTC
   Tue Aug 09 15:45:18.223 2016 PDT | checkpoint record is at 0/90002E0
   Tue Aug 09 15:45:18.223 2016 PDT | redo record is at 0/90002A8; shutdown FALSE
   Tue Aug 09 15:45:18.223 2016 PDT | next transaction ID: 0/1879; next OID: 24578
   Tue Aug 09 15:45:18.223 2016 PDT | next MultiXactId: 1; next MultiXactOffset: 0
   Tue Aug 09 15:45:18.223 2016 PDT | oldest unfrozen transaction ID: 1822, in database 1
   (7 rows)
   ```

### Upgrading PLV8<a name="PostgreSQL.Concepts.General.UpgradingPLv8"></a>

PLV8 is a trusted Javascript language extension for PostgreSQL\. You can use it for stored procedures, triggers, and other procedural code that's callable from SQL\. This language extension is supported by all current releases of PostgreSQL\. 

If you use [PLV8](https://plv8.github.io/) and upgrade PostgreSQL to a new PLV8 version, you immediately take advantage of the new extension\. Take the following steps to synchronize your catalog metadata with the new version of PLV8\. These steps are optional, but we highly recommended that you complete them to avoid metadata mismatch warnings\.

The upgrade process drops all your existing PLV8 functions, so we recommend that you create a snapshot of your RDS for PostgreSQL DB instance before upgrading\. For more information, see [Creating a DB snapshot](USER_CreateSnapshot.md)\.

**To synchronize your catalog metadata with a new version of PLV8**

1. Verify that you need to update\. To do this, run the following command while connected to your instance\.

   ```
   SELECT * FROM pg_available_extensions WHERE name IN ('plv8','plls','plcoffee');
   ```

   If your results contain values for an installed version that is a lower number than the default version, continue with this procedure to update your extensions\. For example, the following result set indicates that you should update\.

   ```
   name    | default_version | installed_version |                     comment
   --------+-----------------+-------------------+--------------------------------------------------
   plls    | 2.1.0           | 1.5.3             | PL/LiveScript (v8) trusted procedural language
   plcoffee| 2.1.0           | 1.5.3             | PL/CoffeeScript (v8) trusted procedural language
   plv8    | 2.1.0           | 1.5.3             | PL/JavaScript (v8) trusted procedural language
   (3 rows)
   ```

1. Create a snapshot of your RDS for PostgreSQL DB instance if you haven't done so yet\. You can continue with the following steps while the snapshot is being created\. 

1. Get a count of the number of PLV8 functions in your DB instance so you can validate that they are all in place after the upgrade\. For example, the following SQL query returns the number of functions written in plv8, plcoffee, and plls\.

   ```
   SELECT proname, nspname, lanname 
   FROM pg_proc p, pg_language l, pg_namespace n
   WHERE p.prolang = l.oid
   AND n.oid = p.pronamespace
   AND lanname IN ('plv8','plcoffee','plls');
   ```

1. Use pg\_dump to create a schema\-only dump file\. For example, create a file on your client machine in the `/tmp` directory\.

   ```
   ./pg_dump -Fc --schema-only -U master postgres >/tmp/test.dmp
   ```

   This example uses the following options:
   + \-FC "format custom"
   + \-\-schema\-only "will only dump commands necessary to create schema \(functions in our case\)"
   + \-U "rds master username"
   + database "the database name in our instance"

   For more information on pg\_dump, see the [pg\_dump](https://www.postgresql.org/docs/current/static/app-pgdump.html ) page in the PostgreSQL documentation\.

1. Extract the "CREATE FUNCTION" DDL statement that is present in the dump file\. The following example uses the `grep` command to extract the DDL statement that creates the functions and save them to a file\. You use this in subsequent steps to recreate the functions\. 

   ```
   ./pg_restore -l /tmp/test.dmp | grep FUNCTION > /tmp/function_list/
   ```

   For more information on pg\_restore see, [pg\_restore](https://www.postgresql.org/docs/current/static/app-pgrestore.html)\. 

1. Drop the functions and extensions\. The following example drops any PLV8 based objects\. The cascade option ensures that any dependent are dropped\.

   ```
   DROP EXTENSION pvl8 CASCADE;
   ```

   If your PostgreSQL instance contains objects based on plcoffee or plls, repeat this step for those extensions\.

1. Create the extensions\. The following example creates the plv8, plcoffee, and plls extensions\.

   ```
   CREATE EXTENSION plv8;
   CREATE EXTENSION plcoffee;
   CREATE EXTENSION plls;
   ```

1. Create the functions using the dump file and "driver" file\.

   The following example recreates the functions that you extracted previously\.

   ```
   ./pg_restore -U master -d postgres -Fc -L /tmp/function_list /tmp/test.dmp
   ```

1. Verify that all your functions have been recreated by using the following query\. 

   ```
   SELECT * FROM pg_available_extensions WHERE name IN ('plv8','plls','plcoffee'); 
   ```

   The PLV8 version 2 adds the following extra row to your result set:

   ```
       proname    |  nspname   | lanname
   ---------------+------------+----------
    plv8_version  | pg_catalog | plv8
   ```

### Logical replication for RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport.LogicalReplication"></a>

Starting with version 10\.4, RDS for PostgreSQL supports the publication and subscription SQL syntax for PostgreSQL 10 Logical Replication\.

**To enable logical replication for an RDS for PostgreSQL DB instance**

1. The AWS user account requires the **rds\_superuser** role to perform logical replication for the PostgreSQL database on Amazon RDS\.

1. Set the `rds.logical_replication` static parameter to 1\. 

1. Modify the inbound rules of the security group for the publisher instance \(production\) to allow the subscriber instance \(replica\) to connect\. This is usually done by including the IP address of the subscriber in the security group\.

1. Restart the DB instance for the changes to the static parameter `rds.logical_replication` to take effect\. 

For more information on PostgreSQL logical replication, see the [PostgreSQL documentation](https://www.postgresql.org/docs/10/static/logical-replication.html)\. 

**Topics**
+ [Logical decoding and logical replication](#PostgreSQL.Concepts.General.FeatureSupport.LogicalDecoding)
+ [Working with logical replication slots](#PostgreSQL.Concepts.General.FeatureSupport.LogicalReplicationSlots)

#### Logical decoding and logical replication<a name="PostgreSQL.Concepts.General.FeatureSupport.LogicalDecoding"></a>

RDS for PostgreSQL supports the streaming of WAL changes using PostgreSQL's logical replication slots\. It also supports using logical decoding\. You can set up logical replication slots on your instance and stream database changes through these slots to a client such as `pg_recvlogical`\. Logical replication slots are created at the database level and support replication connections to a single database\. 

The most common clients for PostgreSQL logical replication are the AWS Database Migration Service or a custom\-managed host on an Amazon EC2 instance\. The logical replication slot knows nothing about the receiver of the stream, and there is no requirement that the target be a replica database\. If you set up a logical replication slot and don't read from the slot, data can be written and quickly fill up your DB instance's storage\.

PostgreSQL logical replication and logical decoding on Amazon RDS are enabled with a parameter, a replication connection type, and a security role\. The client for logical decoding can be any client that is capable of establishing a replication connection to a database on a PostgreSQL DB instance\. 

**To enable logical decoding for an RDS for PostgreSQL DB instance**

1. The user account requires the **rds\_superuser** role to enable logical replication\. The user account also requires the **rds\_replication** role to grant permissions to manage logical slots and to stream data using logical slots\.

1. Set the `rds.logical_replication` static parameter to 1\. As part of applying this parameter, we also set the parameters `wal_level`, `max_wal_senders`, `max_replication_slots`, and `max_connections`\. These parameter changes can increase WAL generation, so you should only set the `rds.logical_replication` parameter when you are using logical slots\.

1. Reboot the DB instance for the static `rds.logical_replication` parameter to take effect\.

1. Create a logical replication slot as explained in the next section\. This process requires that you specify a decoding plugin\. Currently we support the `test_decoding` and `wal2json` output plugins that ship with PostgreSQL\.

For more information on PostgreSQL logical decoding, see the [ PostgreSQL documentation](https://www.postgresql.org/docs/current/static/logicaldecoding-explanation.html)\.

#### Working with logical replication slots<a name="PostgreSQL.Concepts.General.FeatureSupport.LogicalReplicationSlots"></a>

You can use SQL commands to work with logical slots\. For example, the following command creates a logical slot named `test_slot` using the default PostgreSQL output plugin `test_decoding`\.

```
SELECT * FROM pg_create_logical_replication_slot('test_slot', 'test_decoding');
slot_name    | xlog_position
-----------------+---------------
regression_slot | 0/16B1970
(1 row)
```

To list logical slots, use the following command\.

```
SELECT * FROM pg_replication_slots;
```

To drop a logical slot, use the following command\.

```
SELECT pg_drop_replication_slot('test_slot');
pg_drop_replication_slot
-----------------------
(1 row)
```

For more examples on working with logical replication slots, see [ Logical decoding examples](https://www.postgresql.org/docs/9.5/static/logicaldecoding-example.html) in the PostgreSQL documentation\.

After you create the logical replication slot, you can start streaming\. The following example shows how logical decoding is controlled over the streaming replication protocol\. This uses the program `pg_recvlogical`, which is included in the PostgreSQL distribution\. This requires that client authentication is set up to allow replication connections\.

```
pg_recvlogical -d postgres --slot test_slot -U postgres
    --host -instance-name.111122223333.aws-region.rds.amazonaws.com 
    -f -  --start
```

To see the contents of the `pg_replication_origin_status` view, query the `pg_show_replication_origin_status()` function\.

```
SELECT * FROM pg_show_replication_origin_status();
local_id | external_id | remote_lsn | local_lsn
----------+-------------+------------+-----------
(0 rows)
```

### Event triggers for RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport.EventTriggers"></a>

All current PostgreSQL versions support event triggers, and so do all available versions of RDS for PostgreSQL\. You can use the main user account \(default, `postgres`\) to create, modify, rename, and delete event triggers\. Event triggers are at the DB instance level, so they can apply to all databases on an instance\.

For example, the following code creates an event trigger that prints the current user at the end of every DDL command\.

```
CREATE OR REPLACE FUNCTION raise_notice_func()
    RETURNS event_trigger
    LANGUAGE plpgsql AS
$$
BEGIN
    RAISE NOTICE 'In trigger function: %', current_user;
END;
$$;

CREATE EVENT TRIGGER event_trigger_1 
    ON ddl_command_end
EXECUTE PROCEDURE raise_notice_func();
```

For more information about PostgreSQL event triggers, see [Event triggers](https://www.postgresql.org/docs/current/static/event-triggers.html) in the PostgreSQL documentation\.

There are several limitations to using PostgreSQL event triggers on Amazon RDS\. These include:
+ You cannot create event triggers on read replicas\. You can, however, create event triggers on a read replica source\. The event triggers are then copied to the read replica\. The event triggers on the read replica don't fire on the read replica when changes are pushed from the source\. However, if the read replica is promoted, the existing event triggers fire when database operations occur\.
+ To perform a major version upgrade to a PostgreSQL DB instance that uses event triggers, you must delete the event triggers before you upgrade the instance\.

### Huge pages for RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport.HugePages"></a>

Huge pages are a memory management feature that reduces overhead when a database instance is working with large contiguous chunks of memory, such as that used by shared buffers\. This PostgreSQL feature is supported by all currently available RDS for PostgreSQL versions\. You allocate huge pages for your application by using calls to `mmap` or `SYSV` shared memory\. RDS for PostgreSQL supports both 4\-KB and 2\-MB page sizes\. 

Huge pages can be disabled or enabled by the changing the value of the `huge_pages` parameter\. The feature is enabled by default for all DB instance classes other than micro, small, and medium DB instance classes\.

**Note**  
Huge pages aren't supported for db\.m1, db\.m2, and db\.m3 DB instance classes\.

RDS for PostgreSQL uses huge pages based on the available shared memory\. If the DB instance can't use huge pages due to shared memory constraints, Amazon RDS prevents the DB instance from starting\. In this case, Amazon RDS sets the status of the DB instance to an incompatible parameters state\. If this occurs, you can set the `huge_pages` parameter to `off` to allow Amazon RDS to start the DB instance\.

The `shared_buffers` parameter is key to setting the shared memory pool that is required for using huge pages\. The default value for the `shared_buffers` parameter uses a database parameters macro\. This macro sets a percentage of the total 8 KB pages available for the DB instance's memory\. When you use huge pages, those pages are located with the huge pages\. Amazon RDS puts a DB instance into an incompatible parameters state if the shared memory parameters are set to require more than 90 percent of the DB instance memory\.

To learn more about PostgreSQL memory management, see [Resource Consumption](https://www.postgresql.org/docs/current/static/runtime-config-resource.html) in the PostgreSQL documentation\.

### Tablespaces for RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport.Tablespaces"></a>

RDS for PostgreSQL supports tablespaces for compatibility\. Because all storage is on a single logical volume, you can't use tablespaces for IO splitting or isolation\. Our benchmarks and experience indicate that a single logical volume is the best setup for most use cases\. 

To create and use tablespaces with your RDS for PostgreSQL DB instance requires the `rds_superuser` role\. Your RDS for PostgreSQL DB instance's main user account \(default name, `postgres`\) is a member of this role\. For more information, see [Understanding the rds\_superuser role](Appendix.PostgreSQL.CommonDBATasks.md#Appendix.PostgreSQL.CommonDBATasks.Roles)\. 

If you specify a file name when you create a tablespace, the path prefix is `/rdsdbdata/db/base/tablespace`\. The following example places tablespace files in `/rdsdbdata/db/base/tablespace/data`\. This example assumes that a `dbadmin` user \(role\) exists and that it's been granted the `rds_superuser` role needed to work with tablespaces\.

```
postgres=> CREATE TABLESPACE act_data
  OWNER dbadmin
  LOCATION '/data';
CREATE TABLESPACE
```

To learn more about PostgreSQL tablespaces, see [Tablespaces](https://www.postgresql.org/docs/current/manage-ag-tablespaces.html) in the PostgreSQL documentation\.

### Autovacuum for RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport.Autovacuum"></a>

The PostgreSQL autovacuum feature is turned on by default for new PostgreSQL DB instances\. Autovacuum is optional, but we highly recommend that you do not turn autovacuum off\. For more information on using autovacuum with RDS for PostgreSQL, see [Working with PostgreSQL autovacuum on Amazon RDS](Appendix.PostgreSQL.CommonDBATasks.Autovacuum.md)\.

### RAM disk for the stats\_temp\_directory<a name="PostgreSQL.Concepts.General.FeatureSupport.RamDisk"></a>

You can use the RDS for PostgreSQL parameter, `rds.pg_stat_ramdisk_size`, to specify the system memory allocated to a RAM disk for storing the PostgreSQL `stats_temp_directory`\. The RAM disk parameter is available for all PostgreSQL versions on Amazon RDS\. 

Under certain workloads, setting this parameter can improve performance and decrease IO requirements\. For more information about the `stats_temp_directory`, see [ the PostgreSQL documentation\.](https://www.postgresql.org/docs/current/static/runtime-config-statistics.html#GUC-STATS-TEMP-DIRECTORY)\.

To enable a RAM disk for your `stats_temp_directory`, set the `rds.pg_stat_ramdisk_size` parameter to a non\-zero value in the parameter group used by your DB instance\. The parameter value is in MB\. You must reboot the DB instance before the change takes effect\. For information about setting parameters, see [Working with DB parameter groups](USER_WorkingWithParamGroups.md)\.

For example, the following AWS CLI command sets the RAM disk parameter to 256 MB\.

```
aws rds modify-db-parameter-group \
    --db-parameter-group-name pg-95-ramdisk-testing \
    --parameters "ParameterName=rds.pg_stat_ramdisk_size, ParameterValue=256, ApplyMethod=pending-reboot"
```

After you reboot, run the following command to see the status of the `stats_temp_directory`:

```
postgres=> SHOW stats_temp_directory;
```

 The command should return the following: 

```
stats_temp_directory
---------------------------
/rdsdbramdisk/pg_stat_tmp
(1 row)
```

### ALTER ENUM for RDS for PostgreSQL<a name="PostgreSQL.Concepts.General.FeatureSupport.AlterEnum"></a>

PostgreSQL supports creating and altering enumerations\. To learn more, see 

The following code shows an example of altering an enum value\.

```
postgres=> CREATE TYPE rainbow AS ENUM ('red', 'orange', 'yellow', 'green', 'blue', 'purple');
CREATE TYPE
postgres=> CREATE TABLE t1 (colors rainbow);
CREATE TABLE
postgres=> INSERT INTO t1 VALUES ('red'), ( 'orange');
INSERT 0 2
postgres=> SELECT * from t1;
colors
--------
red
orange
(2 rows)
postgres=> ALTER TYPE rainbow RENAME VALUE 'red' TO 'crimson';
ALTER TYPE
postgres=> SELECT * from t1;
colors
---------
crimson
orange
(2 rows)
```
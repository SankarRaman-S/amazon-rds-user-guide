# Overview of Database Activity Streams<a name="DBActivityStreams.Overview"></a>

As an RDS for Oracle database administrator, you need to safeguard your database and meet compliance and regulatory requirements\. One strategy is to integrate database activity streams with your monitoring tools\. In this way, you monitor and set alarms for auditing activity in your Oracle database\.

Security threats are both external and internal\. To protect against internal threats, you can control administrator access to data streams by configuring the Database Activity Streams feature\. RDS for Oracle DBAs don't have access to the collection, transmission, storage, and processing of the streams\.

**Topics**
+ [How database activity streams work](#DBActivityStreams.Overview.how-they-work)
+ [Unified auditing in Oracle Database](#DBActivityStreams.Overview.unified-auditing)
+ [Asynchronous mode for database activity streams](#DBActivityStreams.Overview.sync-mode)
+ [Requirements for database activity streams](#DBActivityStreams.Overview.requirements)
+ [Supported RDS for Oracle engine versions for database activity streams](#DBActivityStreams.Overview.requirements.version)
+ [Supported DB instance classes for database activity streams](#DBActivityStreams.Overview.requirements.classes)
+ [Supported AWS Regions for database activity streams](#DBActivityStreams.Overview.requirements.Regions)

## How database activity streams work<a name="DBActivityStreams.Overview.how-they-work"></a>

Amazon RDS pushes activities to an Amazon Kinesis data stream in near real time\. The Kinesis stream is created automatically\. From Kinesis, you can configure AWS services such as Amazon Kinesis Data Firehose and AWS Lambda to consume the stream and store the data\.

**Important**  
Use of the Database Activity Streams feature in Amazon Aurora and Amazon RDS is free, but Amazon Kinesis charges for a data stream\. For more information, see [Amazon Kinesis Data Streams pricing](https://aws.amazon.com/kinesis/data-streams/pricing/)\.

Applications for compliance management can also consume database activity streams\. These applications can use the stream to generate alerts and audit activity on your Oracle database\.



## Unified auditing in Oracle Database<a name="DBActivityStreams.Overview.unified-auditing"></a>

Amazon RDS for Oracle doesn't capture database activity by default\. You create and manage audit policies in Oracle Database yourself\.

Auditing is the monitoring and recording of configured database actions\. In an Oracle database, a *unified audit policy* is a named group of audit settings that you can use to audit an aspect of user behavior\. A policy can be as simple as auditing the activities of a single user\. You can also create complex audit policies that use conditions\.

An Oracle database writes audit records, including `SYS` audit records, to the *unified audit trail*\. For example, if an error occurs during an `INSERT` statement, standard auditing indicates the error number and the SQL that was executed\. The audit trail resides in a read\-only table in the `AUDSYS` schema\. To access these records, query the `UNIFIED_AUDIT_TRAIL` data dictionary view\.

Typically, you configure database activity streams as follows:

1. Create an Oracle Database audit policy by using the `CREATE AUDIT POLICY` command\.

   The Oracle Database generates audit records\.

1. Enable the audit policy by using the `AUDIT POLICY` command\.

1. Configure database activity streams\.

   Only activities that match the Oracle Database audit policies are captured and sent to the Amazon Kinesis data stream\. When database activity streams are enabled, an Oracle database administrator can't alter the audit policy or remove audit logs\.

To learn more about unified audit policies, see [About Auditing Activities with Unified Audit Policies and AUDIT](https://docs.oracle.com/en/database/oracle/oracle-database/19/dbseg/configuring-audit-policies.html#GUID-2435D929-10AD-43C7-8A6C-5133170074D0) in the *Oracle Database Security Guide*\.

**Topics**
+ [Non\-native audit fields](#DBActivityStreams.Overview.unified-auditing.non-native)
+ [DB parameter group override](#DBActivityStreams.Overview.unified-auditing.parameter-group)

### Non\-native audit fields<a name="DBActivityStreams.Overview.unified-auditing.non-native"></a>

When you start a database activity stream, every database event generates a corresponding activity stream event\. For example, a database user might run `SELECT` and `INSERT` statements\. The database audits these events and sends them to an Amazon Kinesis data stream\.

The events are represented in the stream as JSON objects\. A JSON object contains a `DatabaseActivityMonitoringRecord`, which contains a `databaseActivityEventList` array\. Predefined fields in the array include `class`, `clientApplication`, and `command`\.

Most events in the unified audit trail for Oracle Database map to fields in the RDS data activity stream\. For example, the `UNIFIED_AUDIT_TRAIL.SQL_TEXT` field in unified auditing maps to the `commandText` field in a database activity stream\. However, Oracle Database audit fields such as `OS_USERNAME` don't map to predefined fields in a database activity stream\.

By default, an activity stream doesn't include engine\-native audit fields\. You can configure RDS for Oracle so that it includes these extra fields in the `engineNativeAuditFields` JSON object\.

### DB parameter group override<a name="DBActivityStreams.Overview.unified-auditing.parameter-group"></a>

Typically, you turn on unified auditing in RDS for Oracle by attaching a parameter group\. However, Database Activity Streams would require additional configuration\. To improve your customer experience, Amazon RDS does the following
+ If you enable an activity stream, RDS for Oracle ignores the auditing parameters in the parameter group\. 
+ If you disable an activity stream, RDS for Oracle stops ignoring the auditing parameters\.

## Asynchronous mode for database activity streams<a name="DBActivityStreams.Overview.sync-mode"></a>

Activity streams in RDS for Oracle are always asynchronous\. When a database session generates an activity stream event, the session returns to normal activities immediately\. In the background, the activity stream event is made a durable record\. If an error occurs in the background task, Amazon RDS generates an event\. This event indicates the beginning and end of any time windows where activity stream event records might have been lost\. Asynchronous mode favors database performance over the accuracy of the activity stream\.

## Requirements for database activity streams<a name="DBActivityStreams.Overview.requirements"></a>

In RDS for Oracle, database activity streams have the following requirements and limitations\.

**Topics**
+ [General requirements](#DBActivityStreams.Overview.requirements.misc)
+ [Oracle feature requirements](#DBActivityStreams.Overview.requirements.oracle)

### General requirements<a name="DBActivityStreams.Overview.requirements.misc"></a>
+ Database activity streams require use of Amazon Kinesis\.
+ Database activity streams require use of AWS Key Management Service \(AWS KMS\)\. AWS KMS is required because the activity streams are always encrypted\.
+ Do not encrypt your Amazon Kinesis data stream\. This extra layer of encryption is incompatible with your database activity stream, which is already encrypted with your AWS KMS key\.

### Oracle feature requirements<a name="DBActivityStreams.Overview.requirements.oracle"></a>

RDS for Oracle has the following requirements for database activity streams:
+ CDBs aren't supported\.
+ Oracle read replicas aren't supported\.
+ In an RDS for Oracle DB instance, you create and manage audit policies yourself\. Unlike Amazon Aurora, RDS for Oracle doesn't capture database activities by default\.

## Supported RDS for Oracle engine versions for database activity streams<a name="DBActivityStreams.Overview.requirements.version"></a>

Database activity streams are supported for Oracle Database 19c using version 19\.0\.0\.0\.ru\-2019\-07\.rur\-2019\-07\.r1 and higher\. Your database can use either Enterprise Edition or Standard Edition 2 \(SE2\)\.

## Supported DB instance classes for database activity streams<a name="DBActivityStreams.Overview.requirements.classes"></a>

For Oracle for RDS, you can use database activity streams with the following DB instance classes:
+ db\.m4
+ db\.m5\.\*
+ db\.r4
+ db\.r5\.\*
+ db\.z1d
+ 
**Note**  
The memory optimized db\.r5 classes, which use the naming pattern db\.r5\.*instance\_size*\.tpc*threads\_per\_core*\.mem*ratio*, aren't supported\.

For more information about instance class types, see [DB instance classes](Concepts.DBInstanceClass.md)\.

## Supported AWS Regions for database activity streams<a name="DBActivityStreams.Overview.requirements.Regions"></a>

Database activity streams are supported in all AWS Regions except the following:
+ China \(Beijing\) Region, `cn-north-1`
+ China \(Ningxia\) Region, `cn-northwest-1`
+ AWS GovCloud \(US\-East\), `us-gov-east-1`
+ AWS GovCloud \(US\-West\), `us-gov-west-1`
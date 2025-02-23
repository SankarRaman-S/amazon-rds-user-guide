# Importing and exporting SQL Server databases using native backup and restore<a name="SQLServer.Procedural.Importing"></a>

Amazon RDS supports native backup and restore for Microsoft SQL Server databases using full backup files \(\.bak files\)\. When you use RDS, you access files stored in Amazon S3 rather than using the local file system on the database server\.

For example, you can create a full backup from your local server, store it on S3, and then restore it onto an existing Amazon RDS DB instance\. You can also make backups from RDS, store them on S3, and then restore them wherever you want\.

Native backup and restore is available in all AWS Regions for Single\-AZ and Multi\-AZ DB instances, including Multi\-AZ DB instances with read replicas\. Native backup and restore is available for all editions of Microsoft SQL Server supported on Amazon RDS\.

The following diagram shows the supported scenarios\.

![\[Native Backup and Restore Architecture\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/SQL-bak-file.png)

Using native \.bak files to back up and restore databases is usually the fastest way to back up and restore databases\. There are many additional advantages to using native backup and restore\. For example, you can do the following:
+ Migrate databases to or from Amazon RDS\.
+ Move databases between RDS for SQL Server DB instances\.
+ Migrate data, schemas, stored procedures, triggers, and other database code inside \.bak files\.
+ Backup and restore single databases, instead of entire DB instances\.
+ Create copies of databases for development, testing, training, and demonstrations\.
+ Store and transfer backup files with Amazon S3, for an added layer of protection for disaster recovery\.
+ Create native backups of databases that have Transparent Data Encryption \(TDE\) turned on, and restore those backups to on\-premises databases\. For more information, see [Support for Transparent Data Encryption in SQL Server](Appendix.SQLServer.Options.TDE.md)\.
+ Restore native backups of on\-premises databases that have TDE turned on to RDS for SQL Server DB instances\. For more information, see [Support for Transparent Data Encryption in SQL Server](Appendix.SQLServer.Options.TDE.md)\.

**Contents**
+ [Limitations and recommendations](#SQLServer.Procedural.Importing.Native.Limitations)
+ [Setting up for native backup and restore](#SQLServer.Procedural.Importing.Native.Enabling)
  + [Manually creating an IAM role for native backup and restore](#SQLServer.Procedural.Importing.Native.Enabling.IAM)
+ [Using native backup and restore](#SQLServer.Procedural.Importing.Native.Using)
  + [Backing up a database](#SQLServer.Procedural.Importing.Native.Using.Backup)
    + [Usage](#SQLServer.Procedural.Importing.Native.Backup.Syntax)
    + [Examples](#SQLServer.Procedural.Importing.Native.Backup.Examples)
  + [Restoring a database](#SQLServer.Procedural.Importing.Native.Using.Restore)
    + [Usage](#SQLServer.Procedural.Importing.Native.Restore.Syntax)
    + [Examples](#SQLServer.Procedural.Importing.Native.Restore.Examples)
  + [Restoring a log](#SQLServer.Procedural.Importing.Native.Restore.Log)
    + [Usage](#SQLServer.Procedural.Importing.Native.Restore.Log.Syntax)
    + [Examples](#SQLServer.Procedural.Importing.Native.Restore.Log.Examples)
  + [Finishing a database restore](#SQLServer.Procedural.Importing.Native.Finish.Restore)
    + [Usage](#SQLServer.Procedural.Importing.Native.Finish.Restore.Syntax)
  + [Working with partially restored databases](#SQLServer.Procedural.Importing.Native.Partially.Restored)
    + [Dropping a partially restored database](#SQLServer.Procedural.Importing.Native.Drop.Partially.Restored)
    + [Snapshot restore and point\-in\-time recovery behavior for partially restored databases](#SQLServer.Procedural.Importing.Native.Snapshot.Restore)
  + [Canceling a task](#SQLServer.Procedural.Importing.Native.Using.Cancel)
    + [Usage](#SQLServer.Procedural.Importing.Native.Cancel.Syntax)
  + [Tracking the status of tasks](#SQLServer.Procedural.Importing.Native.Tracking)
    + [Usage](#SQLServer.Procedural.Importing.Native.Tracking.Syntax)
    + [Examples](#SQLServer.Procedural.Importing.Native.Tracking.Examples)
    + [Response](#SQLServer.Procedural.Importing.Native.Tracking.Response)
+ [Compressing backup files](#SQLServer.Procedural.Importing.Native.Compression)
+ [Troubleshooting](#SQLServer.Procedural.Importing.Native.Troubleshooting)
+ [Importing and exporting SQL Server data using other methods](SQLServer.Procedural.Importing.Snapshots.md)
  + [Importing data into RDS for SQL Server by using a snapshot](SQLServer.Procedural.Importing.Snapshots.md#SQLServer.Procedural.Importing.Procedure)
    + [Import the data](SQLServer.Procedural.Importing.Snapshots.md#ImportData.SQLServer.Import)
      + [Generate and Publish Scripts Wizard](SQLServer.Procedural.Importing.Snapshots.md#ImportData.SQLServer.MgmtStudio.ScriptWizard)
      + [Import and Export Wizard](SQLServer.Procedural.Importing.Snapshots.md#ImportData.SQLServer.MgmtStudio.ImportExportWizard)
      + [Bulk copy](SQLServer.Procedural.Importing.Snapshots.md#ImportData.SQLServer.MgmtStudio.BulkCopy)
  + [Exporting data from RDS for SQL Server](SQLServer.Procedural.Importing.Snapshots.md#SQLServer.Procedural.Exporting)
    + [SQL Server Import and Export Wizard](SQLServer.Procedural.Importing.Snapshots.md#SQLServer.Procedural.Exporting.SSIEW)
    + [SQL Server Generate and Publish Scripts Wizard and bcp utility](SQLServer.Procedural.Importing.Snapshots.md#SQLServer.Procedural.Exporting.SSGPSW)

## Limitations and recommendations<a name="SQLServer.Procedural.Importing.Native.Limitations"></a>

The following are some limitations to using native backup and restore: 
+ You can't back up to, or restore from, an Amazon S3 bucket in a different AWS Region from your Amazon RDS DB instance\.
+ You can't restore a database with the same name as an existing database\. Database names are unique\.
+ We strongly recommend that you don't restore backups from one time zone to a different time zone\. If you restore backups from one time zone to a different time zone, you must audit your queries and applications for the effects of the time zone change\.
+ Amazon S3 has a size limit of 5 TB per file\. For native backups of larger databases, you can use multifile backup\.
+ The maximum database size that can be backed up to S3 depends on the available memory, CPU, I/O, and network resources on the DB instance\. The larger the database, the more memory the backup agent consumes\. Our testing shows that you can make a compressed backup of a 16\-TB database on our newest\-generation instance types from `2xlarge` instance sizes and larger, given sufficient system resources\.
+ You can't back up to or restore from more than 10 backup files at the same time\.
+ A differential backup is based on the last full backup\. For differential backups to work, you can't take a snapshot between the last full backup and the differential backup\. If you want a differential backup, but a manual or automated snapshot exists, then do another full backup before proceeding with the differential backup\.
+ Differential and log restores aren't supported for databases with files that have their file\_guid \(unique identifier\) set to `NULL`\.
+ You can run up to two backup or restore tasks at the same time\.
+ You can't perform native log backups from SQL Server on Amazon RDS\.
+ RDS supports native restores of databases up to 16 TB\. Native restores of databases on SQL Server Express Edition are limited to 10 GB\.
+ You can't do a native backup during the maintenance window, or any time Amazon RDS is in the process of taking a snapshot of the database\. If a native backup task overlaps with the RDS daily backup window, the native backup task is canceled\.
+ On Multi\-AZ DB instances, you can only natively restore databases that are backed up in the full recovery model\.
+ Restoring from differential backups on Multi\-AZ instances isn't supported\.
+ Calling the RDS procedures for native backup and restore within a transaction isn't supported\.
+ Use a symmetric encryption AWS KMS key to encrypt your backups\. Amazon RDS doesn't support asymmetric KMS keys\. For more information, see [Creating symmetric encryption KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk) in the *AWS Key Management Service Developer Guide*\.
+ Native backup files are encrypted with the specified KMS key using the "Encryption\-Only" crypto mode\. When you are restoring encrypted backup files, be aware that they were encrypted with the "Encryption\-Only" crypto mode\.
+ You can't restore a database that contains a FILESTREAM file group\.

If your database can be offline while the backup file is created, copied, and restored, we recommend that you use native backup and restore to migrate it to RDS\. If your on\-premises database can't be offline, we recommend that you use the AWS Database Migration Service to migrate your database to Amazon RDS\. For more information, see [What is AWS Database Migration Service?](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html) 

Native backup and restore isn't intended to replace the data recovery capabilities of the cross\-region snapshot copy feature\. We recommend that you use snapshot copy to copy your database snapshot to another AWS Region for cross\-region disaster recovery in Amazon RDS\. For more information, see [Copying a DB snapshot](USER_CopySnapshot.md)\.

## Setting up for native backup and restore<a name="SQLServer.Procedural.Importing.Native.Enabling"></a>

To set up for native backup and restore, you need three components:

1. An Amazon S3 bucket to store your backup files\.

   You must have an S3 bucket to use for your backup files and then upload backups you want to migrate to RDS\. If you already have an Amazon S3 bucket, you can use that\. If you don't, you can [create a bucket](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/CreatingaBucket.html)\. Alternatively, you can choose to have a new bucket created for you when you add the `SQLSERVER_BACKUP_RESTORE` option by using the AWS Management Console\.

   For information on using S3, see the *Amazon Simple Storage Service User Guide* for a simple introduction\. For more depth, see the *Amazon Simple Storage Service User Guide*\.

1. An AWS Identity and Access Management \(IAM\) role to access the bucket\.

   If you already have an IAM role, you can use that\. You can choose to have a new IAM role created for you when you add the `SQLSERVER_BACKUP_RESTORE` option by using the AWS Management Console\. Alternatively, you can create a new one manually\.

   If you want to create a new IAM role manually, take the approach discussed in the next section\. Do the same if you want to attach trust relationships and permissions policies to an existing IAM role\.

1. The `SQLSERVER_BACKUP_RESTORE` option added to an option group on your DB instance\.

   To enable native backup and restore on your DB instance, you add the `SQLSERVER_BACKUP_RESTORE` option to an option group on your DB instance\. For more information and instructions, see [Support for native backup and restore in SQL Server](Appendix.SQLServer.Options.BackupRestore.md)\.

### Manually creating an IAM role for native backup and restore<a name="SQLServer.Procedural.Importing.Native.Enabling.IAM"></a>

If you want to manually create a new IAM role to use with native backup and restore, you can do so\. In this case, you create a role to delegate permissions from the Amazon RDS service to your Amazon S3 bucket\. When you create an IAM role, you attach a trust relationship and a permissions policy\. The trust relationship allows RDS to assume this role\. The permissions policy defines the actions this role can perform\. For more information about creating the role, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)\.

For the native backup and restore feature, use trust relationships and permissions policies similar to the examples in this section\. In the following example, we use the service principal name `rds.amazonaws.com` as an alias for all service accounts\. In the other examples, we specify an Amazon Resource Name \(ARN\) to identify another account, user, or role that we're granting access to in the trust policy\.

We recommend using the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys in resource\-based trust relationships to limit the service's permissions to a specific resource\. This is the most effective way to protect against the [confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html)\.

You might use both global condition context keys and have the `aws:SourceArn` value contain the account ID\. In this case, the `aws:SourceAccount` value and the account in the `aws:SourceArn` value must use the same account ID when used in the same statement\.
+ Use `aws:SourceArn` if you want cross\-service access for a single resource\.
+ Use `aws:SourceAccount` if you want to allow any resource in that account to be associated with the cross\-service use\.

In the trust relationship, make sure to use the `aws:SourceArn` global condition context key with the full ARN of the resources accessing the role\. For native backup and restore, make sure to include both the DB option group and the DB instances, as shown in the following example\.

**Example trust relationship with global condition context key for native backup and restore**  

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "rds.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceArn": [
                        "arn:aws:rds:Region:my_account_ID:db:db_instance_identifier",
                        "arn:aws:rds:Region:my_account_ID:og:option_group_name"
                    ]
                }
            }
        }
    ]
}
```

The following example uses an ARN to specify a resource\. For more information on using ARNs, see [ Amazon resource names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\. 

**Example permissions policy for native backup and restore without encryption support**  

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement":
 4.     [
 5.         {
 6.         "Effect": "Allow",
 7.         "Action":
 8.             [
 9.                 "s3:ListBucket",
10.                 "s3:GetBucketLocation"
11.             ],
12.         "Resource": "arn:aws:s3:::bucket_name"
13.         },
14.         {
15.         "Effect": "Allow",
16.         "Action":
17.             [
18.                 "s3:GetObjectMetaData",
19.                 "s3:GetObject",
20.                 "s3:PutObject",
21.                 "s3:ListMultipartUploadParts",
22.                 "s3:AbortMultipartUpload"
23.             ],
24.         "Resource": "arn:aws:s3:::bucket_name/*"
25.         }
26.     ]
27. }
```

**Example permissions policy for native backup and restore with encryption support**  
If you want to encrypt your backup files, include an encryption key in your permissions policy\. For more information about encryption keys, see [Getting started](https://docs.aws.amazon.com/kms/latest/developerguide/getting-started.html) in the *AWS Key Management Service Developer Guide*\.  
You must use a symmetric encryption KMS key to encrypt your backups\. Amazon RDS doesn't support asymmetric KMS keys\. For more information, see [Creating symmetric encryption KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk) in the *AWS Key Management Service Developer Guide*\.  
The IAM role must also be a key user and key administrator for the KMS key, that is, it must be specified in the key policy\. For more information, see [Creating symmetric encryption KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk) in the *AWS Key Management Service Developer Guide*\.

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement":
 4.     [
 5.         {
 6.         "Effect": "Allow",
 7.         "Action":
 8.             [
 9.                 "kms:DescribeKey",
10.                 "kms:GenerateDataKey",
11.                 "kms:Encrypt",
12.                 "kms:Decrypt"
13.             ],
14.         "Resource": "arn:aws:kms:region:account-id:key/key-id"
15.         },
16.         {
17.         "Effect": "Allow",
18.         "Action":
19.             [
20.                 "s3:ListBucket",
21.                 "s3:GetBucketLocation"
22.             ],
23.         "Resource": "arn:aws:s3:::bucket_name"
24.         },
25.         {
26.         "Effect": "Allow",
27.         "Action":
28.             [
29.                 "s3:GetObjectMetaData",
30.                 "s3:GetObject",
31.                 "s3:PutObject",
32.                 "s3:ListMultipartUploadParts",
33.                 "s3:AbortMultipartUpload"
34.             ],
35.         "Resource": "arn:aws:s3:::bucket_name/*"
36.         }
37.     ]
38. }
```

## Using native backup and restore<a name="SQLServer.Procedural.Importing.Native.Using"></a>

After you have enabled and configured native backup and restore, you can start using it\. First, you connect to your Microsoft SQL Server database, and then you call an Amazon RDS stored procedure to do the work\. For instructions on connecting to your database, see [Connecting to a DB instance running the Microsoft SQL Server database engine](USER_ConnectToMicrosoftSQLServerInstance.md)\. 

Some of the stored procedures require that you provide an Amazon Resource Name \(ARN\) to your Amazon S3 bucket and file\. The format for your ARN is `arn:aws:s3:::bucket_name/file_name.extension`\. Amazon S3 doesn't require an account number or AWS Region in ARNs\.

If you also provide an optional KMS key, the format for the ARN of the key is `arn:aws:kms:region:account-id:key/key-id`\. For more information, see [ Amazon resource names \(ARNs\) and AWS service namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\. You must use a symmetric encryption KMS key to encrypt your backups\. Amazon RDS doesn't support asymmetric KMS keys\. For more information, see [Creating symmetric encryption KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk) in the *AWS Key Management Service Developer Guide*\.

**Note**  
Whether or not you use a KMS key, the native backup and restore tasks enable server\-side Advanced Encryption Standard \(AES\) 256\-bit encryption by default for files uploaded to S3\.

For instructions on how to call each stored procedure, see the following topics:
+ [Backing up a database](#SQLServer.Procedural.Importing.Native.Using.Backup)
+ [Restoring a database](#SQLServer.Procedural.Importing.Native.Using.Restore)
+ [Restoring a log](#SQLServer.Procedural.Importing.Native.Restore.Log)
+ [Finishing a database restore](#SQLServer.Procedural.Importing.Native.Finish.Restore)
+ [Working with partially restored databases](#SQLServer.Procedural.Importing.Native.Partially.Restored)
+ [Canceling a task](#SQLServer.Procedural.Importing.Native.Using.Cancel)
+ [Tracking the status of tasks](#SQLServer.Procedural.Importing.Native.Tracking)

### Backing up a database<a name="SQLServer.Procedural.Importing.Native.Using.Backup"></a>

To back up your database, use the `rds_backup_database` stored procedure\.

**Note**  
You can't back up a database during the maintenance window, or while Amazon RDS is taking a snapshot\. 

#### Usage<a name="SQLServer.Procedural.Importing.Native.Backup.Syntax"></a>

```
exec msdb.dbo.rds_backup_database
	@source_db_name='database_name',
	@s3_arn_to_backup_to='arn:aws:s3:::bucket_name/file_name.extension',
	[@kms_master_key_arn='arn:aws:kms:region:account-id:key/key-id'],	
	[@overwrite_s3_backup_file=0|1],
	[@type='DIFFERENTIAL|FULL'],
	[@number_of_files=n];
```

The following parameters are required:
+ `@source_db_name` – The name of the database to back up\.
+ `@s3_arn_to_backup_to` – The ARN indicating the Amazon S3 bucket to use for the backup, plus the name of the backup file\.

  The file can have any extension, but `.bak` is usually used\. 

The following parameters are optional:
+ `@kms_master_key_arn` – The ARN for the symmetric encryption KMS key to use to encrypt the item\.
  + You can't use the default encryption key\. If you use the default key, the database won't be backed up\.
  +  If you don't specify a KMS key identifier, the backup file won't be encrypted\. For more information, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html)\.
  + When you specify a KMS key, client\-side encryption is used\.
  + Amazon RDS doesn't support asymmetric KMS keys\. For more information, see [Creating symmetric encryption KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk) in the *AWS Key Management Service Developer Guide*\.
+ `@overwrite_s3_backup_file` – A value that indicates whether to overwrite an existing backup file\.
  + `0` – Doesn't overwrite an existing file\. This value is the default\.

    Setting `@overwrite_s3_backup_file` to 0 returns an error if the file already exists\.
  + `1` – Overwrites an existing file that has the specified name, even if it isn't a backup file\.
+ `@type` – The type of backup\.
  + `DIFFERENTIAL` – Makes a differential backup\.
  + `FULL` – Makes a full backup\. This value is the default\.

  A differential backup is based on the last full backup\. For differential backups to work, you can't take a snapshot between the last full backup and the differential backup\. If you want a differential backup, but a snapshot exists, then do another full backup before proceeding with the differential backup\.

  You can look for the last full backup or snapshot using the following example SQL query:

  ```
  select top 1
  database_name
  , 	backup_start_date
  , 	backup_finish_date
  from    msdb.dbo.backupset
  where   database_name='mydatabase'
  and     type = 'D'
  order by backup_start_date desc;
  ```
+ `@number_of_files` – The number of files into which the backup will be divided \(chunked\)\. The maximum number is 10\.
  + Multifile backup is supported for both full and differential backups\.
  + If you enter a value of 1 or omit the parameter, a single backup file is created\.

  Provide the prefix that the files have in common, then suffix that with an asterisk \(`*`\)\. The asterisk can be anywhere in the *file\_name* part of the S3 ARN\. The asterisk is replaced by a series of alphanumeric strings in the generated files, starting with `1-of-number_of_files`\.

  For example, if the file names in the S3 ARN are `backup*.bak` and you set `@number_of_files=4`, the backup files generated are `backup1-of-4.bak`, `backup2-of-4.bak`, `backup3-of-4.bak`, and `backup4-of-4.bak`\.
  + If any of the file names already exists, and `@overwrite_s3_backup_file` is 0, an error is returned\.
  + Multifile backups can only have one asterisk in the *file\_name* part of the S3 ARN\.
  + Single\-file backups can have any number of asterisks in the *file\_name* part of the S3 ARN\. Asterisks aren't removed from the generated file name\.

#### Examples<a name="SQLServer.Procedural.Importing.Native.Backup.Examples"></a>

**Example of differential backup**  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup1.bak',
@overwrite_s3_backup_file=1,
@type='DIFFERENTIAL';
```

**Example of full backup with encryption**  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup1.bak',
@kms_master_key_arn='arn:aws:kms:us-east-1:123456789012:key/AKIAIOSFODNN7EXAMPLE',
@overwrite_s3_backup_file=1,
@type='FULL';
```

**Example of multifile backup**  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup*.bak',
@number_of_files=4;
```

**Example of multifile differential backup**  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup*.bak',
@type='DIFFERENTIAL',
@number_of_files=4;
```

**Example of multifile backup with encryption**  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup*.bak',
@kms_master_key_arn='arn:aws:kms:us-east-1:123456789012:key/AKIAIOSFODNN7EXAMPLE',
@number_of_files=4;
```

**Example of multifile backup with S3 overwrite**  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup*.bak',
@overwrite_s3_backup_file=1,
@number_of_files=4;
```

**Example of single\-file backup with the @number\_of\_files parameter**  
This example generates a backup file named `backup*.bak`\.  

```
exec msdb.dbo.rds_backup_database
@source_db_name='mydatabase',
@s3_arn_to_backup_to='arn:aws:s3:::mybucket/backup*.bak',
@number_of_files=1;
```

### Restoring a database<a name="SQLServer.Procedural.Importing.Native.Using.Restore"></a>

To restore your database, call the `rds_restore_database` stored procedure\. Amazon RDS creates an initial snapshot of the database after the restore task is complete and the database is open\.

#### Usage<a name="SQLServer.Procedural.Importing.Native.Restore.Syntax"></a>

```
exec msdb.dbo.rds_restore_database
	@restore_db_name='database_name',
	@s3_arn_to_restore_from='arn:aws:s3:::bucket_name/file_name.extension',
	@with_norecovery=0|1,
	[@kms_master_key_arn='arn:aws:kms:region:account-id:key/key-id'],
	[@type='DIFFERENTIAL|FULL'];
```

The following parameters are required:
+ `@restore_db_name` – The name of the database to restore\. Database names are unique\. You can't restore a database with the same name as an existing database\.
+ `@s3_arn_to_restore_from` – The ARN indicating the Amazon S3 prefix and names of the backup files used to restore the database\.
  + For a single\-file backup, provide the entire file name\.
  + For a multifile backup, provide the prefix that the files have in common, then suffix that with an asterisk \(`*`\)\.
  + If `@s3_arn_to_restore_from` is empty, the following error message is returned: S3 ARN prefix cannot be empty\.

The following parameter is required for differential restores, but optional for full restores:
+ `@with_norecovery` – The recovery clause to use for the restore operation\.
  + Set it to `0` to restore with RECOVERY\. In this case, the database is online after the restore\.
  + Set it to `1` to restore with NORECOVERY\. In this case, the database remains in the RESTORING state after restore task completion\. With this approach, you can do later differential restores\.
  + For DIFFERENTIAL restores, specify `0` or `1`\.
  + For `FULL` restores, this value defaults to `0`\.

The following parameters are optional:
+ `@kms_master_key_arn` – If you encrypted the backup file, the KMS key to use to decrypt the file\.

  When you specify a KMS key, client\-side encryption is used\.
+ `@type` – The type of restore\. Valid types are `DIFFERENTIAL` and `FULL`\. The default value is `FULL`\.

**Note**  
For differential restores, either the database must be in the RESTORING state or a task must already exist that restores with NORECOVERY\.  
You can't restore later differential backups while the database is online\.  
You can't submit a restore task for a database that already has a pending restore task with RECOVERY\.  
Full restores with NORECOVERY and differential restores aren't supported on Multi\-AZ instances\.  
Restoring a database on a Multi\-AZ instance with read replicas is similar to restoring a database on a Multi\-AZ instance\. You don't have to take any additional actions to restore a database on a replica\.

#### Examples<a name="SQLServer.Procedural.Importing.Native.Restore.Examples"></a>

**Example of single\-file restore**  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak';
```

**Example of multifile restore**  
To avoid errors when restoring multiple files, make sure that all the backup files have the same prefix, and that no other files use that prefix\.  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup*';
```

**Example of full database restore with RECOVERY**  
The following three examples perform the same task, full restore with RECOVERY\.  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak';
```

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak',
[@type='DIFFERENTIAL|FULL'];
```

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak',
@type='FULL',
@with_norecovery=0;
```

**Example of full database restore with encryption**  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak',
@kms_master_key_arn='arn:aws:kms:us-east-1:123456789012:key/AKIAIOSFODNN7EXAMPLE';
```

**Example of full database restore with NORECOVERY**  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak',
@type='FULL',
@with_norecovery=1;
```

**Example of differential restore with NORECOVERY**  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak',
@type='DIFFERENTIAL',
@with_norecovery=1;
```

**Example of differential restore with RECOVERY**  

```
exec msdb.dbo.rds_restore_database
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/backup1.bak',
@type='DIFFERENTIAL',
@with_norecovery=0;
```

### Restoring a log<a name="SQLServer.Procedural.Importing.Native.Restore.Log"></a>

To restore your log, call the `rds_restore_log` stored procedure\.

#### Usage<a name="SQLServer.Procedural.Importing.Native.Restore.Log.Syntax"></a>

```
exec msdb.dbo.rds_restore_log 
	@restore_db_name='database_name',
	@s3_arn_to_restore_from='arn:aws:s3:::bucket_name/log_file_name.extension',
	[@kms_master_key_arn='arn:aws:kms:region:account-id:key/key-id'],
	[@with_norecovery=0|1],
	[@stopat='datetime'];
```

The following parameters are required:
+ `@restore_db_name` – The name of the database whose log to restore\.
+ `@s3_arn_to_restore_from` – The ARN indicating the Amazon S3 prefix and name of the log file used to restore the log\. The file can have any extension, but `.trn` is usually used\.

  If `@s3_arn_to_restore_from` is empty, the following error message is returned: S3 ARN prefix cannot be empty\.

The following parameters are optional:
+ `@kms_master_key_arn` – If you encrypted the log, the KMS key to use to decrypt the log\.
+ `@with_norecovery` – The recovery clause to use for the restore operation\. This value defaults to `1`\.
  + Set it to `0` to restore with RECOVERY\. In this case, the database is online after the restore\. You can't restore further log backups while the database is online\.
  + Set it to `1` to restore with NORECOVERY\. In this case, the database remains in the RESTORING state after restore task completion\. With this approach, you can do later log restores\.
+ `@stopat` – A value that specifies that the database is restored to its state at the date and time specified \(in datetime format\)\. Only transaction log records written before the specified date and time are applied to the database\.

  If this parameter isn't specified \(it is NULL\), the complete log is restored\.

**Note**  
For log restores, either the database must be in a state of restoring or a task must already exist that restores with NORECOVERY\.  
You can't restore log backups while the database is online\.  
You can't submit a log restore task on a database that already has a pending restore task with RECOVERY\.  
Log restores aren't supported on Multi\-AZ instances\.

#### Examples<a name="SQLServer.Procedural.Importing.Native.Restore.Log.Examples"></a>

**Example of log restore**  

```
exec msdb.dbo.rds_restore_log
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/mylog.trn';
```

**Example of log restore with encryption**  

```
exec msdb.dbo.rds_restore_log
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/mylog.trn',
@kms_master_key_arn='arn:aws:kms:us-east-1:123456789012:key/AKIAIOSFODNN7EXAMPLE';
```

**Example of log restore with NORECOVERY**  
The following two examples perform the same task, log restore with NORECOVERY\.  

```
exec msdb.dbo.rds_restore_log
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/mylog.trn',
@with_norecovery=1;
```

```
exec msdb.dbo.rds_restore_log
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/mylog.trn';
```

**Example of log restore with RECOVERY**  

```
exec msdb.dbo.rds_restore_log
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/mylog.trn',
@with_norecovery=0;
```

**Example of log restore with STOPAT clause**  

```
exec msdb.dbo.rds_restore_log
@restore_db_name='mydatabase',
@s3_arn_to_restore_from='arn:aws:s3:::mybucket/mylog.trn',
@with_norecovery=0,
@stopat='2019-12-01 03:57:09';
```

### Finishing a database restore<a name="SQLServer.Procedural.Importing.Native.Finish.Restore"></a>

If the last restore task on the database was performed using `@with_norecovery=1`, the database is now in the RESTORING state\. Open this database for normal operation by using the `rds_finish_restore` stored procedure\.

#### Usage<a name="SQLServer.Procedural.Importing.Native.Finish.Restore.Syntax"></a>

```
exec msdb.dbo.rds_finish_restore @db_name='database_name';
```

**Note**  
To use this approach, the database must be in the RESTORING state without any pending restore tasks\.  
The `rds_finish_restore` procedure isn't supported on Multi\-AZ instances\.  
To finish restoring the database, use the master login\. Or use the user login that most recently restored the database or log with NORECOVERY\.

### Working with partially restored databases<a name="SQLServer.Procedural.Importing.Native.Partially.Restored"></a>

#### Dropping a partially restored database<a name="SQLServer.Procedural.Importing.Native.Drop.Partially.Restored"></a>

To drop a partially restored database \(left in the RESTORING state\), use the `rds_drop_database` stored procedure\.

```
exec msdb.dbo.rds_drop_database @db_name='database_name';
```

**Note**  
You can't submit a DROP database request for a database that already has a pending restore or finish restore task\.  
To drop the database, use the master login\. Or use the user login that most recently restored the database or log with NORECOVERY\.

#### Snapshot restore and point\-in\-time recovery behavior for partially restored databases<a name="SQLServer.Procedural.Importing.Native.Snapshot.Restore"></a>

Partially restored databases in the source instance \(left in the RESTORING state\) are dropped from the target instance during snapshot restore and point\-in\-time recovery\.

### Canceling a task<a name="SQLServer.Procedural.Importing.Native.Using.Cancel"></a>

To cancel a backup or restore task, call the `rds_cancel_task` stored procedure\.

**Note**  
You can't cancel a FINISH\_RESTORE task\.

#### Usage<a name="SQLServer.Procedural.Importing.Native.Cancel.Syntax"></a>

```
exec msdb.dbo.rds_cancel_task @task_id=ID_number;
```

The following parameter is required:
+ `@task_id` – The ID of the task to cancel\. You can get the task ID by calling `rds_task_status`\. 

### Tracking the status of tasks<a name="SQLServer.Procedural.Importing.Native.Tracking"></a>

To track the status of your backup and restore tasks, call the `rds_task_status` stored procedure\. If you don't provide any parameters, the stored procedure returns the status of all tasks\. The status for tasks is updated approximately every two minutes\. Task history is retained for 36 days\.

#### Usage<a name="SQLServer.Procedural.Importing.Native.Tracking.Syntax"></a>

```
exec msdb.dbo.rds_task_status
	[@db_name='database_name'],
	[@task_id=ID_number];
```

The following parameters are optional: 
+ `@db_name` – The name of the database to show the task status for\.
+ `@task_id` – The ID of the task to show the task status for\.

#### Examples<a name="SQLServer.Procedural.Importing.Native.Tracking.Examples"></a>

**Example of listing the status for a specific task**  

```
exec msdb.dbo.rds_task_status @task_id=5;
```

**Example of listing the status for a specific database and task**  

```
exec msdb.dbo.rds_task_status
@db_name='my_database',
@task_id=5;
```

**Example of listing all tasks and their statuses on a specific database**  

```
exec msdb.dbo.rds_task_status @db_name='my_database';
```

**Example of listing all tasks and their statuses on the current instance**  

```
exec msdb.dbo.rds_task_status;
```

#### Response<a name="SQLServer.Procedural.Importing.Native.Tracking.Response"></a>

The `rds_task_status` stored procedure returns the following columns\.


****  

| Column | Description | 
| --- | --- | 
| `task_id` |  The ID of the task\.   | 
| `task_type` |  Task type depending on the input parameters, as follows: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.html) Amazon RDS creates an initial snapshot of the database after it is open on completion of the following restore tasks: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.html)  | 
| `database_name` |  The name of the database that the task is associated with\.   | 
| `% complete` |  The progress of the task as a percent value\.   | 
| `duration (mins)` |  The amount of time spent on the task, in minutes\.   | 
| `lifecycle` |  The status of the task\. The possible statuses are the following:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.html)  | 
| `task_info` |  Additional information about the task\.  If an error occurs while backing up or restoring a database, this column contains information about the error\. For a list of possible errors, and mitigation strategies, see [Troubleshooting](#SQLServer.Procedural.Importing.Native.Troubleshooting)\.   | 
| `last_updated` |  The date and time that the task status was last updated\. The status is updated after every 5 percent of progress\.  | 
| `created_at` | The date and time that the task was created\. | 
| S3\_object\_arn | The ARN indicating the Amazon S3 prefix and the name of the file that is being backed up or restored\. | 
| `overwrite_s3_backup_file` |  The value of the `@overwrite_s3_backup_file` parameter specified when calling a backup task\. For more information, see [Backing up a database](#SQLServer.Procedural.Importing.Native.Using.Backup)\.  | 
| KMS\_master\_key\_arn | The ARN for the KMS key used for encryption \(for backup\) and decryption \(for restore\)\. | 
| filepath | Not applicable to native backup and restore tasks\. | 
| overwrite\_file | Not applicable to native backup and restore tasks\. | 

## Compressing backup files<a name="SQLServer.Procedural.Importing.Native.Compression"></a>

To save space in your Amazon S3 bucket, you can compress your backup files\. For more information about compressing backup files, see [Backup compression](https://msdn.microsoft.com/en-us/library/bb964719.aspx) in the Microsoft documentation\. 

Compressing your backup files is supported for the following database editions: 
+ Microsoft SQL Server Enterprise Edition 
+ Microsoft SQL Server Standard Edition 

To turn on compression for your backup files, run the following code:

```
1. exec rdsadmin..rds_set_configuration 'S3 backup compression', 'true';
```

To turn off compression for your backup files, run the following code: 

```
1. exec rdsadmin..rds_set_configuration 'S3 backup compression', 'false';
```

## Troubleshooting<a name="SQLServer.Procedural.Importing.Native.Troubleshooting"></a>

The following are issues you might encounter when you use native backup and restore\.


****  

| Issue | Troubleshooting suggestions | 
| --- | --- | 
|  Database backup/restore option is not enabled yet or is in the process of being enabled\. Please try again later\.  |  Make sure that you have added the `SQLSERVER_BACKUP_RESTORE` option to the DB option group associated with your DB instance\. For more information, see [Adding the native backup and restore option](Appendix.SQLServer.Options.BackupRestore.md#Appendix.SQLServer.Options.BackupRestore.Add)\.  | 
|  Access Denied  | The backup or restore process can't access the backup file\. This is usually caused by issues like the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.html)  | 
|  BACKUP DATABASE WITH COMPRESSION isn't supported on <edition\_name> Edition  |  Compressing your backup files is only supported for Microsoft SQL Server Enterprise Edition and Standard Edition\. For more information, see [Compressing backup files](#SQLServer.Procedural.Importing.Native.Compression)\.   | 
|  Key <ARN> does not exist  |  You attempted to restore an encrypted backup, but didn't provide a valid encryption key\. Check your encryption key and retry\. For more information, see [Restoring a database](#SQLServer.Procedural.Importing.Native.Using.Restore)\.   | 
|  Please reissue task with correct type and overwrite property  |  If you attempt to back up your database and provide the name of a file that already exists, but set the overwrite property to false, the save operation fails\. To fix this error, either provide the name of a file that doesn't already exist, or set the overwrite property to true\. For more information, see [Backing up a database](#SQLServer.Procedural.Importing.Native.Using.Backup)\. It's also possible that you intended to restore your database, but called the `rds_backup_database` stored procedure accidentally\. In that case, call the `rds_restore_database` stored procedure instead\. For more information, see [Restoring a database](#SQLServer.Procedural.Importing.Native.Using.Restore)\. If you intended to restore your database and called the `rds_restore_database` stored procedure, make sure that you provided the name of a valid backup file\. For more information, see [Using native backup and restore](#SQLServer.Procedural.Importing.Native.Using)\.  | 
|  Please specify a bucket that is in the same region as RDS instance  |  You can't back up to, or restore from, an Amazon S3 bucket in a different AWS Region from your Amazon RDS DB instance\. You can use Amazon S3 replication to copy the backup file to the correct AWS Region\. For more information, see [Cross\-Region replication](https://docs.aws.amazon.com/AmazonS3/latest/dev/crr.html) in the Amazon S3 documentation\.  | 
|  The specified bucket does not exist  | Verify that you have provided the correct ARN for your bucket and file, in the correct format\.  For more information, see [Using native backup and restore](#SQLServer.Procedural.Importing.Native.Using)\.  | 
|  User <ARN> is not authorized to perform <kms action> on resource <ARN>  |  You requested an encrypted operation, but didn't provide correct AWS KMS permissions\. Verify that you have the correct permissions, or add them\.  For more information, see [Setting up for native backup and restore](#SQLServer.Procedural.Importing.Native.Enabling)\.  | 
|  The Restore task is unable to restore from more than 10 backup file\(s\)\. Please reduce the number of files matched and try again\.  |  Reduce the number of files that you're trying to restore from\. You can make each individual file larger if necessary\.   | 
|  Database '*database\_name*' already exists\. Two databases that differ only by case or accent are not allowed\. Choose a different database name\.  |  You can't restore a database with the same name as an existing database\. Database names are unique\.  | 
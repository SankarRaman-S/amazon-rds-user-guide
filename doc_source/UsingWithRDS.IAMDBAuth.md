# IAM database authentication for MariaDB, MySQL, and PostgreSQL<a name="UsingWithRDS.IAMDBAuth"></a>

You can authenticate to your DB instance using AWS Identity and Access Management \(IAM\) database authentication\. IAM database authentication works with MariaDB, MySQL and PostgreSQL\. With this authentication method, you don't need to use a password when you connect to a DB instance\. Instead, you use an authentication token\.

An *authentication token* is a unique string of characters that Amazon RDS generates on request\. Authentication tokens are generated using AWS Signature Version 4\. Each token has a lifetime of 15 minutes\. You don't need to store user credentials in the database, because authentication is managed externally using IAM\. You can also still use standard database authentication\. The token is only used for authentication and doesn't affect the session after it is established\.

IAM database authentication provides the following benefits:
+ Network traffic to and from the database is encrypted using Secure Socket Layer \(SSL\) or Transport Layer Security \(TLS\)\. For more information about using SSL/TLS with Amazon RDS, see [Using SSL/TLS to encrypt a connection to a DB instance](UsingWithRDS.SSL.md)\.
+ You can use IAM to centrally manage access to your database resources, instead of managing access individually on each DB instance\.
+ For applications running on Amazon EC2, you can use profile credentials specific to your EC2 instance to access your database instead of a password, for greater security\.

**Topics**
+ [Availability for IAM database authentication](#UsingWithRDS.IAMDBAuth.Availability)
+ [Limitations for IAM database authentication](#UsingWithRDS.IAMDBAuth.Limitations)
+ [MariaDB and MySQL recommendations for IAM database authentication](#UsingWithRDS.IAMDBAuth.ConnectionsPerSecond)
+ [Enabling and disabling IAM database authentication](UsingWithRDS.IAMDBAuth.Enabling.md)
+ [Creating and using an IAM policy for IAM database access](UsingWithRDS.IAMDBAuth.IAMPolicy.md)
+ [Creating a database account using IAM authentication](UsingWithRDS.IAMDBAuth.DBAccounts.md)
+ [Connecting to your DB instance using IAM authentication](UsingWithRDS.IAMDBAuth.Connecting.md)

## Availability for IAM database authentication<a name="UsingWithRDS.IAMDBAuth.Availability"></a>

IAM database authentication is available for the following database engines:
+ MariaDB 10\.6, all minor versions
+ MySQL 8\.0, minor version 8\.0\.16 or higher
+ MySQL 5\.7, minor version 5\.7\.16 or higher
+ PostgreSQL 14, 13, 12, and 11, all minor versions
+ PostgreSQL 10, minor version 10\.6 or higher
+ PostgreSQL 9\.6, minor version 9\.6\.11 or higher
+ PostgreSQL 9\.5, minor version 9\.5\.15 or higher

IAM database authentication is available for the [AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/rds/generate-db-auth-token.html) and for the following language\-specific AWS SDKs:
+ [AWS SDK for \.NET](https://docs.aws.amazon.com/sdkfornet/v3/apidocs/items/RDS/TRDSAuthTokenGenerator.html)
+ [AWS SDK for C\+\+](https://sdk.amazonaws.com/cpp/api/LATEST/class_aws_1_1_r_d_s_1_1_r_d_s_client.html#ae134ffffed5d7672f6156d324e7bd392)
+ [AWS SDK for Go](https://docs.aws.amazon.com/sdk-for-go/api/service/rds/#pkg-overview)
+ [AWS SDK for Java](https://docs.aws.amazon.com/sdk-for-java/latest/reference/software/amazon/awssdk/services/rds/RdsUtilities.html)
+ [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/RDS/Signer.html)
+ [AWS SDK for PHP](https://docs.aws.amazon.com/aws-sdk-php/v3/api/class-Aws.Rds.AuthTokenGenerator.html)
+ [AWS SDK for Python \(Boto3\)](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rds.html#RDS.Client.generate_db_auth_token)
+ [AWS SDK for Ruby](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/RDS/AuthTokenGenerator.html)

## Limitations for IAM database authentication<a name="UsingWithRDS.IAMDBAuth.Limitations"></a>

When using IAM database authentication, the following limitations apply:
+ The maximum number of connections per second for your DB instance might be limited depending on its DB instance class and your workload\.
+ Currently, IAM database authentication doesn't support all global condition context keys\.

  For more information about global condition context keys, see [AWS global condition context keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.
+ Currently, IAM database authentication isn't supported for CNAMEs\.
+ For PostgreSQL, if the IAM role \(`rds_iam`\) is added to the master user, IAM authentication takes precedence over Password authentication so the master user has to log in as an IAM user\.

## MariaDB and MySQL recommendations for IAM database authentication<a name="UsingWithRDS.IAMDBAuth.ConnectionsPerSecond"></a>

We recommend the following when using the MariaDB or MySQL DB engine:
+ Use IAM database authentication as a mechanism for temporary, personal access to databases\.
+ Use IAM database authentication only for workloads that can be easily retried\.
+ Use IAM database authentication when your application requires fewer than 200 new IAM database authentication connections per second\.

  The database engines that work with Amazon RDS don't impose any limits on authentication attempts per second\. However, when you use IAM database authentication, your application must generate an authentication token\. Your application then uses that token to connect to the DB instance\. If you exceed the limit of maximum new connections per second, then the extra overhead of IAM database authentication can cause connection throttling\. The extra overhead can cause even existing connections to drop\.  For information about the maximum total connections for MariaDB and MySQL, see [Maximum MySQL and MariaDB connections](CHAP_Troubleshooting.md#USER_ConnectToInstance.max_connections)\.   

**Note**  
These recommendations don't apply to Amazon RDS for PostgreSQL DB instances\.
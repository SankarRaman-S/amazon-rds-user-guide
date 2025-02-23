# Tutorial: Create a web server and an Amazon RDS DB instance<a name="TUT_WebAppWithRDS"></a>

This tutorial helps you install an Apache web server with PHP and create a MySQL database\. The web server runs on an Amazon EC2 instance using Amazon Linux, and the MySQL database is an MySQL DB instance\. Both the Amazon EC2 instance and the DB instance run in a virtual private cloud \(VPC\) based on the Amazon VPC service\. 

**Important**  
There's no charge for creating an AWS account\. However, by completing this tutorial, you might incur costs for the AWS resources you use\. You can delete these resources after you complete the tutorial if they are no longer needed\.

**Note**  
This tutorial works with Amazon Linux and might not work for other versions of Linux such as Ubuntu\.

In the tutorial that follows, you specify the VPC, subnets, and security groups when you create the DB instance\. You also specify them when you create the EC2 instance to host your web server\. The VPC, subnets, and security groups are required for the DB instance and the web server to communicate\. After the VPC is set up, this tutorial shows you how to create the DB instance and install the web server\. You connect your web server to your DB instance in the VPC using the DB instance endpoint endpoint\.

1. Complete the tasks in [Tutorial: Create an Amazon VPC for use with a DB instance \(IPv4 only\)](CHAP_Tutorials.WebServerDB.CreateVPC.md)\.

   Before you begin this tutorial, make sure that you have a VPC with both public and private subnets, and corresponding security groups\. If you don't have these, complete the following tasks in the tutorial: 

   1. [Create a VPC with private and public subnets](CHAP_Tutorials.WebServerDB.CreateVPC.md#CHAP_Tutorials.WebServerDB.CreateVPC.VPCAndSubnets)

   1. [Create a VPC security group for a public web server](CHAP_Tutorials.WebServerDB.CreateVPC.md#CHAP_Tutorials.WebServerDB.CreateVPC.SecurityGroupEC2)

   1. [Create a VPC security group for a private DB instance](CHAP_Tutorials.WebServerDB.CreateVPC.md#CHAP_Tutorials.WebServerDB.CreateVPC.SecurityGroupDB)

   1. [Create a DB subnet group](CHAP_Tutorials.WebServerDB.CreateVPC.md#CHAP_Tutorials.WebServerDB.CreateVPC.DBSubnetGroup)

1. [Create a DB instance](CHAP_Tutorials.WebServerDB.CreateDBInstance.md)

1. [Create an EC2 instance and install a web server](CHAP_Tutorials.WebServerDB.CreateWebServer.md)

The following diagram shows the configuration when the tutorial is complete\.

![\[Single VPC Scenario\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/con-VPC-sec-grp.png)
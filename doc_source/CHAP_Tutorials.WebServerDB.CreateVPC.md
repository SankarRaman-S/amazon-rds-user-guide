# Tutorial: Create an Amazon VPC for use with a DB instance \(IPv4 only\)<a name="CHAP_Tutorials.WebServerDB.CreateVPC"></a>

A common scenario includes a DB instance in an Amazon VPC, that shares data with a web server that is running in the same VPC\. In this tutorial you create the VPC for this scenario\. 

The following diagram shows this scenario\. For information about other scenarios, see [Scenarios for accessing a DB instance in a VPC](USER_VPC.Scenarios.md)\. 

 

![\[Single VPC Scenario\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/con-VPC-sec-grp.png)

Because your DB instance only needs to be available to your web server, and not to the public Internet, you create a VPC with both public and private subnets\. The web server is hosted in the public subnet, so that it can reach the public Internet\. The DB instance is hosted in a private subnet\. The web server is able to connect to the DB instance because it is hosted within the same VPC, but the DB instance is not available to the public Internet, providing greater security\. 

This tutorial describes configuring a VPC for Amazon RDS DB instances\. For more information about Amazon VPC, see [Amazon VPC Getting Started Guide](https://docs.aws.amazon.com/AmazonVPC/latest/GettingStartedGuide/) and [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

**Note**  
For a tutorial that shows you how to create a web server for this VPC scenario, see [Tutorial: Create a web server and an Amazon RDS DB instance](TUT_WebAppWithRDS.md)\.

## Create a VPC with private and public subnets<a name="CHAP_Tutorials.WebServerDB.CreateVPC.VPCAndSubnets"></a>

Use the following procedure to create a VPC with both public and private subnets\. 

**To create a VPC and subnets**

1. If you don't have an Elastic IP address to associate with a network address translation \(NAT\) gateway, allocate one now\. A NAT gateway is required for this tutorial\. If you have an available Elastic IP address, move on to the next step\.

   1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

   1. In the top\-right corner of the AWS Management Console, choose the Region to allocate your Elastic IP address in\. The Region of your Elastic IP address should be the same as the Region where you want to create your VPC\. This example uses the US West \(Oregon\) Region\.

   1. In the navigation pane, choose **Elastic IPs**\.

   1. Choose **Allocate Elastic IP address**\.

   1. If the console shows the **Network Border Group** field, keep the default value for it\.

   1. For **Public IPv4 address pool**, choose **Amazon's pool of IPv4 addresses**\.

   1. Choose **Allocate**\.

      Note the allocation ID of the new Elastic IP address because you'll need this information when you create your VPC\.

   For more information about Elastic IP addresses, see [Elastic IP addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) in the *Amazon EC2 User Guide*\. For more information about NAT gateways, see [NAT gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) in the *Amazon VPC User Guide*\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the top\-right corner of the AWS Management Console, choose the Region to create your VPC in\. This example uses the US West \(Oregon\) Region\.

1. In the upper\-left corner, make sure **New VPC Experience** is turned off\.

1. In the upper\-left corner, choose **VPC Dashboard**\. To begin creating a VPC, choose **Launch VPC Wizard**\.

1. On the **Step 1: Select a VPC Configuration** page, choose **VPC with Public and Private Subnets**, and then choose **Select**\.

1. On the **Step 2: VPC with Public and Private Subnets** page, set these values:
   + **IPv4 CIDR block:** `10.0.0.0/16`
   + **IPv6 CIDR block:** No IPv6 CIDR Block
   + **VPC name:** `tutorial-vpc`
   + **Public subnet's IPv4 CIDR:** `10.0.0.0/24`
   + **Availability Zone:** `us-west-2a`
   + **Public subnet name:** `Tutorial public`
   + **Private subnet's IPv4 CIDR:** `10.0.1.0/24`
   + **Availability Zone:** `us-west-2b`
   + **Private subnet name:** `Tutorial private 1` 
   + **Elastic IP Allocation ID:** An Elastic IP address to associate with the NAT gateway
   + **Service endpoints:** Skip this field\.
   + **Enable DNS hostnames:** `Yes`
   + **Hardware tenancy:** `Default`

1. Choose **Create VPC**\.

## Create additional subnets<a name="CHAP_Tutorials.WebServerDB.CreateVPC.AdditionalSubnets"></a>

You must have either two private subnets or two public subnets available to create a DB subnet group for a DB instance to use in a VPC\. Because the DB instance for this tutorial is private, add a second private subnet to the VPC\. 

**To create an additional subnet**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. To add the second private subnet to your VPC, choose **VPC Dashboard**, choose **Subnets**, and then choose **Create subnet**\.

1. On the **Create subnet** page, set these values: 
   + **VPC ID:** Choose the VPC that you created in the previous step, for example: `vpc-identifier (tutorial-vpc)`
   + **Subnet name:** `Tutorial private 2`
   + **Availability Zone:** `us-west-2c` 
**Note**  
Choose an Availability Zone that is different from the one that you chose for the first private subnet\.
   + **IPv4 CIDR block:** `10.0.2.0/24`

1. Choose **Create subnet**\.

1. To ensure that the second private subnet that you created uses the same route table as the first private subnet, complete the following steps:

   1. Choose **VPC Dashboard**, choose **Subnets**, and then choose the first private subnet that you created for the VPC, `Tutorial private 1`\. 

   1. Below the list of subnets, choose the **Route table** tab, and note the value for **Route Table**—for example: `rtb-98b613fd`\. 

   1. In the list of subnets, deselect the first private subnet\.

   1. In the list of subnets, choose the second private subnet `Tutorial private 2`, and choose the **Route table** tab\. 

   1. If the current route table is not the same as the route table for the first private subnet, choose **Edit route table association**\. For **Route table ID**, choose the route table that you noted earlier—for example: `rtb-98b613fd`\. Next, to save your selection, choose **Save**\.

## Create a VPC security group for a public web server<a name="CHAP_Tutorials.WebServerDB.CreateVPC.SecurityGroupEC2"></a>

Next you create a security group for public access\. To connect to public instances in your VPC, you add inbound rules to your VPC security group that allow traffic to connect from the internet\. 

**To create a VPC security group**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **VPC Dashboard**, choose **Security Groups**, and then choose **Create security group**\. 

1. On the **Create security group** page, set these values: 
   + **Security group name:** `tutorial-securitygroup`
   + **Description:** `Tutorial Security Group`
   + **VPC:** Choose the VPC that you created earlier, for example: `vpc-identifier (tutorial-vpc)` 

1. Add inbound rules to the security group\.

   1. Determine the IP address to use to connect to instances in your VPC\. To determine your public IP address, in a different browser window or tab, you can use the service at [https://checkip\.amazonaws\.com](https://checkip.amazonaws.com)\. An example of an IP address is `203.0.113.25/32`\.

      If you are connecting through an Internet service provider \(ISP\) or from behind your firewall without a static IP address, you need to find out the range of IP addresses used by client computers\.
**Warning**  
  
If you use `0.0.0.0/0`, you enable all IP addresses to access your public instances\. This approach is acceptable for a short time in a test environment, but it's unsafe for production environments\. In production, you'll authorize only a specific IP address or range of addresses to access your instances\.

   1. In the **Inbound rules** section, choose **Add rule**\.

   1. Set the following values for your new inbound rule to allow Secure Shell \(SSH\) access to your Amazon EC2 instance\. If you do this, you can connect to your Amazon EC2 instance to install the web server and other utilities, and to upload content for your web server\. 
      + **Type:** `SSH`
      + **Source:** The IP address or range from Step a, for example: `203.0.113.25/32`\.

   1. Choose **Add rule**\.

   1. Set the following values for your new inbound rule to allow HTTP access to your web server\. 
      + **Type:** `HTTP`
      + **Source:** `0.0.0.0/0`

1. To create the security group, choose **Create security group**\.

   Note the security group ID because you need it later in this tutorial\.

## Create a VPC security group for a private DB instance<a name="CHAP_Tutorials.WebServerDB.CreateVPC.SecurityGroupDB"></a>

To keep your DB instance private, create a second security group for private access\. To connect to private instances in your VPC, you add inbound rules to your VPC security group that allow traffic from your web server only\. 

**To create a VPC security group**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **VPC Dashboard**, choose **Security Groups**, and then choose **Create security group**\.

1. On the **Create security group** page, set these values:
   + **Security group name:** `tutorial-db-securitygroup`
   + **Description:** `Tutorial DB Instance Security Group`
   + **VPC:** Choose the VPC that you created earlier, for example: `vpc-identifier (tutorial-vpc)`

1. Add inbound rules to the security group\.

   1. In the **Inbound rules** section, choose **Add rule**\.

   1. Set the following values for your new inbound rule to allow MySQL traffic on port 3306 from your Amazon EC2 instance\. If you do this, you can connect from your web server to your DB instance to store and retrieve data from your web application to your database\. 
      + **Type:** `MySQL/Aurora`
      + **Source:** The identifier of the `tutorial-securitygroup` security group that you created previously in this tutorial, for example: `sg-9edd5cfb`\.

1. To create the security group, choose **Create security group**\.

## Create a DB subnet group<a name="CHAP_Tutorials.WebServerDB.CreateVPC.DBSubnetGroup"></a>

A DB subnet group is a collection of subnets that you create in a VPC and that you then designate for your DB instances\. A DB subnet group allows you to specify a particular VPC when creating DB instances\.

**To create a DB subnet group**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.
**Note**  
Make sure you connect to the Amazon RDS console, not to the Amazon VPC console\.

1. In the navigation pane, choose **Subnet groups**\.

1. Choose **Create DB Subnet Group**\.

1. On the **Create DB subnet group** page, set these values in **Subnet group details**:
   + **Name:** `tutorial-db-subnet-group`
   + **Description:** `Tutorial DB Subnet Group`
   + **VPC:** `tutorial-vpc (vpc-identifier)` 

1. In the **Add subnets** section, choose the **Availability Zones** and **Subnets**\.

   For this tutorial, choose `us-west-2b` and `us-west-2c` for the **Availability Zones**\. Next, for **Subnets**, choose the subnets for IPv4 CIDR block 10\.0\.1\.0/24 and 10\.0\.2\.0/24\.
**Note**  
If you have enabled a Local Zone, you can choose an Availability Zone group on the **Create DB subnet group** page\. In this case, choose the **Availability Zone group**, **Availability Zones**, and **Subnets**\.

1. Choose **Create**\. 

    Your new DB subnet group appears in the DB subnet groups list on the RDS console\. You can click the DB subnet group to see details, including all of the subnets associated with the group, in the details pane at the bottom of the window\.

**Note**  
If you created this VPC to complete [Tutorial: Create a web server and an Amazon RDS DB instance](TUT_WebAppWithRDS.md), create the DB instance by following the instructions in [Create a DB instance](CHAP_Tutorials.WebServerDB.CreateDBInstance.md)\.

## Deleting the VPC<a name="CHAP_Tutorials.WebServerDB.CreateVPC.Delete"></a>

After you create the VPC and other resources for this tutorial, you can delete them if they are no longer needed\.

**Note**  
If you added resources in the Amazon VPC you created for this tutorial, such as Amazon EC2 instances or Amazon RDS DB instances, you might need to delete these resources before you can delete the VPC\. For more information, see [Delete your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#VPC_Deleting) in the *Amazon VPC User Guide*\.

**To delete a VPC and related resources**

1. Delete the DB subnet group\.

   1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

   1. In the navigation pane, choose **Subnet groups**\.

   1. Select the DB subnet group you want to delete, such as **tutorial\-db\-subnet\-group**\.

   1. Choose **Delete**, and then choose **Delete** in the confirmation window\.

1. Note the VPC ID\.

   1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

   1. Choose **VPC Dashboard**, and then choose **VPCs**\.

   1. In the list, identify the VPC you created, such as **tutorial\-vpc**\.

   1. Note the **VPC ID** of the VPC you created\. You will need the VPC ID in subsequent steps\.

1. Delete the security groups\.

   1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

   1. Choose **VPC Dashboard**, and then choose **Security Groups**\.

   1. Select the security group for the Amazon RDS DB instance, such as **tutorial\-db\-securitygroup**\.

   1. From **Actions**, choose **Delete security groups**, and then choose **Delete** on the confirmation page\.

   1. On the **Security Groups** page, select the security group for the Amazon EC2 instance, such as **tutorial\-securitygroup**\.

   1. From **Actions**, choose **Delete security groups**, and then choose **Delete** on the confirmation page\.

1. Delete the NAT gateway\.

   1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

   1. Choose **VPC Dashboard**, and then choose **NAT Gateways**\.

   1. Select the NAT gateway of the VPC you created\. Use the VPC ID to identify the correct NAT gateway\.

   1. From **Actions**, choose **Delete NAT gateway**\.

   1. On the confirmation page, enter **delete**, and then choose **Delete**\.

1. Delete the VPC\.

   1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

   1. Choose **VPC Dashboard**, and then choose **VPCs**\.

   1. Select the VPC you want to delete, such as **tutorial\-vpc**\.

   1. From **Actions**, choose **Delete VPC**\.

      The confirmation page shows other resources that are associated with the VPC that will also be deleted, including the subnets associated with it\.

   1. On the confirmation page, enter **delete**, and then choose **Delete**\.

1. Release the Elastic IP addresses\.

   1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

   1. Choose **Amazon EC2 Dashboard**, and then choose **Elastic IPs**\.

   1. Select the Elastic IP address you want to release\.

   1. From **Actions**, choose **Release Elastic IP addresses**\.

   1. On the confirmation page, choose **Release**\.
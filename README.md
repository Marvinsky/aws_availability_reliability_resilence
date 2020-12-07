# Aws project that guaranties: Hig Availability, High Reliability, and High Resilence

### Create VPC using YAML file.

### Region
![Choose Region](screenshots/IAM_region.png "Choose Region")


<ol>
<li>Services -> CloudFormation</li>
<li>Create stack "With new resources (standard)"</li>
<li>Template is ready</li>
<li>Upload a template file: https://github.com/Marvinsky/aws_availability_reliability_resilence/cloudformation/vpc.yaml</li>
<li>Fill in Stack Name: <b>Primary</b></li>
<li>Name the VPC: <b>Left it empty</b></li>
<li>Update the CIDR blocks</li>
<li>Click Next -> Next Again -> Click create Stack</li>
<li>Wait for the stack to build out. Refresh until status becomes "CREATE_COMPLETE"</li>
</ol>

### Screenshots: Creation CF & VPC
#### Upload YAML file:
![Create VPC](screenshots/cf_creation_00.png "Create VPC")
#### CIDR:
![Create VPC](screenshots/cf_creation_01.png "Create VPC")
#### Outputs:
![Create VPC](screenshots/cf_creation_02.png "Create VPC")
#### Resources:
![Create VPC](screenshots/cf_creation_03.png "Create VPC")


### Data Durability and Recovery

<ol>
<li>Pick two AWS regions. An active and standby region</li>
<li>Use CloudFormation to create one VPC in each region. Name the VPC in the active
region "Primary" and name the VPC in the standby region "Secondary"</li>
</ol>
<b>NOTE:</b> <i>Be sure to use different CIDR address ranges for the VPCs</i>

#### Regions:
<ol>
<li>Oregon - Active Region</li>
<li>N.Virginia - Standby Region</li>
</ol>

#### primary VPC:
![Primary VPC](screenshots/grade/primary_Vpc.png "Primary VPC")
#### primary VPC detail:
![Primary VPC Detail](screenshots/primary_Vpc_detail.png "Primary VPC Detail")

#### secondary VPC:
![Secondary VPC](screenshots/grade/secondary_Vpc.png "Secondary VPC")
#### secondary VPC Detail:
![Secondary VPC Detail](screenshots/secondary_Vpc_detail.png "Secondary VPC Detail")


### Highly durable RDS Database

<ol>
<li>Create a new RDS Subnet group in the active and standby region
using private subnets.</li>
<li>Create a new MySQL, multi-AZ database in the active region. The database must:
    <ul>
        <li>Be a "burstable" instance class.</li>
        <li>Have only the "UDARR-Database" security group.</li>
        <li>Have an initial database called "udacity"</li>
    </ul>
</li>
<li>Create a read replica database in the standby region. This database
has the same requirements as the database in the active region.</li>
</ol>

<b>SAVE</b> screenshots of the configuration of the databases in the active
and secondary region after they are created. Also, save screenshots
of the configuration of the database subnet groups as well as route tables associated
with those subnets. Name the screenshots:

#### Oregon Region

#### VPC
![VPC name](screenshots/VPC_vpcname_oregon.png "VPC name")

#### private subnets
![Private Subnet](screenshots/VPC_privatesubnet_oregon.png "Private Subnet")


#### RDS subnet creation
![RDS Subnet creation](screenshots/RDS_creation_00.png "RDS creation")

#### RDS subnet selected
![RDS Subnet selected](screenshots/RDS_creation_01.png "RDS selected")

#### MYSQL primary private subnet
![RDS Subnet selected](screenshots/MYSQL_primary_privatesubnet.png "RDS selected")

#### MYSQL primary automatic backup enabled
![MYSQL primary automatic backup](screenshots/MYSQL_primary_autobackup_enabled.png "MYSQL primary automatic backup")

#### Private Subnet routing table
![Subnet routing table](screenshots/Subnet_routingtable.png "Subnet routing table")


#### N.Virginia

#### VPC
![VPC name](screenshots/VPC_vpcname_northvirginia.png "VPC name")

#### private subnets
![Private Subnet](screenshots/VPC_privatesubnet_northvirginia.png "Private Subnet")


#### RDS subnet creation
![RDS Subnet creation](screenshots/RDS_creation_00_nvirginia.png "RDS creation")

#### RDS subnet selected
![RDS Subnet selected](screenshots/RDS_creation_01_nvirginia.png "RDS selected")

#### Mysql creation

#### Enable Availability Zone in active region (oregon)
![Availability Zone](screenshots/RDS_mysql_creation_00.png "enable AZ")

#### Be a "burstable"
![Burstable instance](screenshots/RDS_mysql_creation_01.png "Burstable instance")

#### Name it: udacity
![Udacity name](screenshots/RDS_mysql_creation_02.png "Udacity name")

#### Security Group
![Security Group](screenshots/RDS_mysql_creation_03.png "Security Group")

#### <b>Password</b>: <i>12345678</i>

#### MYSQL secondary private subnet
![MySQL secundary](screenshots/MYSQL_secundary_privatesubnet.png "MySQL secundary")

#### MYSQL secondary automatic backup enabled
![MYSQL primary automatic backup](screenshots/MYSQL_secundary_autobackup_enabled.png "MYSQL primary automatic backup")

#### Private secondary Subnet routing table
![Subnet routing table](screenshots/Subnet_secundary_routingtable.png "Subnet routing table")





#### Primary DB config
![Primary DB config](screenshots/grade/primaryDB_config.png "Primary DB config")

#### Secondary DB config
![Secondary DB config](screenshots/grade/secondaryDB_config.png "Secondary DB config")

#### PrimaryDB subnet group
![Primary Subnet Group](screenshots/grade/primaryDB_subnetgroup.png "Primary Subnet Group")

#### SecondaryDB subnet group
![Secondary Subnet Group](screenshots/grade/secondaryDB_subnetgroup.png "Secondary Subnet Group")

#### Primary VPC Subnet
![Primary VPC Subnets](screenshots/grade/primaryVPC_subnets.png "Primary VPC Subnet")

#### Secondary VPC Subnet
![Secondary VPC Subnets](screenshots/grade/secondaryVPC_subnets.png "Secondary VPC Subnet")

#### Primary Subnet Routing
![Primary Subnet Routing](screenshots/grade/primary_subnet_routing.png "Primary Subnet Routing")

#### Secondary Subnet Routing
![Secondary Subnet Routing](screenshots/grade/secondary_subnet_routing.png "Secondary Subnet Routing")

### Availability Estimate

Write a paragraph or two describing the achievable Recovery Time Objective (RTO) and
Recovery Point Objective (RPO) for this Multi-AZ, multi-region database in terms of:

<ol>
<li>Minimum RTO for a single AZ outage</li>
<li>Minimum RTO for a single region outage</li>
<li>Minimum RPO for a single AZ outage</li>
<li>Minimum RPO for a single region outage</li>
</ol>

<b>SAVE:<b/> <i>estimates.txt</i>

https://github.com/Marvinsky/aws_availability_reliability_resilence/estimates.txt

### Demonstrate Normal Usage

In the active region:

<ol>
<li>Create an EC2 keypair in the region</li>
<li>Launch an Amazon Linux EC2 instance in the active region. Configure
the instance to use the VPC's public subnet and security group ("UDARR-Application")</li>
<li>SSH to the instance and connect to the "udacity" database in the RDS instance</li>
<li>Verify that you can create a table, insert data, and read data from the database</li>
<li>You have now demonstrated that you can read and write to the primary database.</li>
</ol>

<b>SAVE</b>: The log connecting to the database, creating the table,
writing to and reading from the table in a text file called <i>log_primary.txt</i>

#### Amazon Linux EC2 - Creation 00
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_00.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 01
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_01.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 02
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_02.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 03
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_03.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 04
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_04.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 05
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_05.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 06
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_06.png "Amazon Linux EC2")

#### Amazon Linux EC2 - Creation 07
![Amazon Linux EC2](screenshots/USAGE_EC2_creation_07.png "Amazon Linux EC2")

<b>SAVE:<b/> <i>log_primary.txt</i>

https://github.com/Marvinsky/aws_availability_reliability_resilence/log_primary.txt

### Monitor database

<ol>
<li>Observe the "DB Connections" to the database and how this metric
changes as you connect to the database</li>
<li>Observe the "Replication" configuration with your multi-region read replica</li>
</ol>

#### Monitor Connection - udacity
![Monitor database](screenshots/grade/monitoring_connections.png "Monitor database")

#### Monitor Replication - udacity
![Monitor database](screenshots/grade/monitoring_replication.png "Monitor database")

### Failover And Recovery

In the standby region

<ol>
<li>Create an EC2 keypair in the region</li>
<li>Launch an Amazon Linux EC2 instance in the standby region. Configure the instance to use the VPC's public subnet and security group ("UDARR-Application").
</li>
<li>SSH to the instance and connect to the read replica database.</li>
<li>Verify if you are not able to insert data into the database but are able to read from the database.</li>
<li>You have now demonstrated that you can only read from the read replica database.</li>
</ol>

<b>SAVE:</b> log_rr_before_promotion.txt

#### RR before promotion
![rr before promotion](screenshots/grade/rr_before_promotion.png "rr before promotion")

#### Promote read replica in order to make insertion
![Read Replica](screenshots/REPLICA_promote.png "Read Replica")

#### RR after promotion
![rr after promotion](screenshots/grade/rr_after_promotion.png "rr after promotion")


### Website Resiliency

Build a resilient static web hosting in AWS. Create a versioned S3 bucket and
configure it as a static website.

<ol>
<li>Enter "index.html" for both index document and Error document</li>
<li>Upload the files from the GitHub repo (under <b>/project/s3/</b>)</li>
<li>Paste URL into a web browser to see your website</li>
</ol>

#### S3 bucket creation
![S3 bucket creation](screenshots/S3_bucket_creation_00.png "S3 bucket creation")

#### S3 bucket enable public access for file.
![S3 bucket creation](screenshots/S3_bucket_creation_01.png "S3 bucket creation")

#### S3 Original
![S3 Original](screenshots/grade/s3_original.png "S3 Original")

#### S3 Season
![S3 Season](screenshots/grade/s3_season.png "S3 Season")

#### S3 Season Revert
![S3 Season Revert](screenshots/grade/s3_season_revert.png "S3 Season Revert")

#### S3 Deletion
![S3 Deletion](screenshots/grade/s3_deletion.png "S3 Deletion")

#### S3 Delete Marker
![S3 Deletion Marker](screenshots/grade/s3_delete_marker.png "S3 Delete Marker")

#### S3 Delete Revert
![S3 Deletion Revert](screenshots/grade/s3_delete_revert.png "S3 Delete Revert")


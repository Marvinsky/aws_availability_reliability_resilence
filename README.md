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
![Primary VPC](screenshots/primary_Vpc.png "Primary VPC")
#### primary VPC detail:
![Primary VPC Detail](screenshots/primary_Vpc_detail.png "Primary VPC Detail")

#### secondary VPC:
![Secondary VPC](screenshots/secondary_Vpc.png "Secondary VPC")
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

Password: 12345678

#### Primary DB config
![Primary DB config](screenshots/primaryDB_config.png "Primary DB config")

#### Secondary DB config
![Secondary DB config](screenshots/secondaryDB_config.png "Secondary DB config")

#### PrimaryDB subnet group
![Primary Subnet Group](screenshots/primaryDB_subnetgroup.png "Primary Subnet Group")

#### SecondaryDB subnet group
![Secondary Subnet Group](screenshots/secondaryDB_subnetgroup.png "Secondary Subnet Group")

#### Primary VPC Subnet
![Primary VPC Subnets](screenshots/primaryVPC_subnets.png "Primary VPC Subnet")

#### Secondary VPC Subnet
![Secondary VPC Subnets](screenshots/secondaryVPC_subnets.png "Secondary VPC Subnet")

#### Primary Subnet Routing
![Primary Subnet Routing](screenshots/primary_subnet_routing.png "Primary Subnet Routing")

#### Secondary Subnet Routing
![Secondary Subnet Routing](screenshots/secondary_subnet_routing.png "Secondary Subnet Routing")

### Availability Estimate

Write a paragraph or two describing the achievable Recovery Time Objective (RTO) and
Recovery Point Objective (RPO) for this Multi-AZ, multi-region database in terms of:

<ol>
<li>Minimum RTO for a single AZ outage</li>
<li>Minimum RTO for a single region outage</li>
<li>Minimum RPO for a single AZ outage</li>
<li>Minimum RPO for a single region outage</li>
</ol>


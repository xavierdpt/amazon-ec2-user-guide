Amazon resources can be: 
- Global
- tied to a Region
- tied to an Availability Zone
- tied to a Local Zone


### Regions<a name="concepts-regions"></a>

Instance can only use AMIs from the same region.
AMIs from other regions must be copied before being used.

Charge for data transfer between Regions
https://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)

### Availability Zones<a name="concepts-availability-zones"></a>

When launching an instance, the availability zone can be set manually or chosen by AWS

Use Elastic IPs to mask the failure of an instance in one Availability Zone by rapidly remapping the address to an instance in another Availability Zone

Naming convention for availability zones: Region code followed by a letter identifier
  example: 'us-east-1a'

The mapping from availability zones to letter identifiers is different from one account to another.

AZ IDs are unique and consistent identifier for an Availability Zone:
example: 'use1-az1' is an AZ ID for the `us-east-1` Region and it has the same location in every AWS account\.

AZ IDs are important when determining if resources on different accounts are on the same AZ.

AWS Local Zones
http://aws.amazon.com/about-aws/global-infrastructure/localzones/

Local Zone identifier: example: 'us-west-2-lax-1a'

Steps:
- enable the local zone
- create a subnet in the local zone
- add resources to the local zone:
  - Amazon EC2 instances
  - Amazon EBS volumes
  - Amazon FSx file servers
  - Application Load Balancer
  - Dedicated Hosts

Local Zones are not available in every regions

Network border group: unique set of Availability Zones or Local Zones from where AWS advertises IP addresses
You can allocate the following resources from a network border group:
+ Elastic IPv4 addresses that Amazon provides
+ IPv6 Amazon\-provided VPC addresses

A network border group limits the addresses to the group.
IP addresses cannot move between network border groups.

## Available Regions<a name="concepts-available-regions"></a>


Regular AWS account: access to multiple regions worlwide
AWS GovCloud: AWS GovCloud Region only
Amazon AWS China: China only

Newer regions must be enabled manually


US
- East
  - Ohio: us-east-2 
  - N. Virginia: us-east-1 
- West
  - N. California: us-west-1 
  - Oregon : us-west-2 
Africa:
  - Cape Town : af-south-1 
Asia Pacific
  - Hong Kong : ap-east-1 
  - Mumbai : ap-south-1 
  - Osaka-Local : ap-northeast-3 
  - Seoul : ap-northeast-2 
  - Singapore : ap-southeast-1 
  - Sydney : ap-southeast-2 
  - Tokyo : ap-northeast-1 
Canada:
- ca-central-1 
Europe:
- Frankfurt: eu-central-1 
- Ireland: eu-west-1 
- London: eu-west-2 
- Milan: eu-south-1 
- Paris: eu-west-3 
- Stockholm: eu-north-1 
Middle East
- Bahrain: me-south-1 
South America:
- São Paulo: sa-east-1 

AWS Global Infrastructure
https://aws.amazon.com/about-aws/global-infrastructure/

## Regions and endpoints<a name="using-regions-endpoints"></a>

Amazon EC2 endpoints and quotas
https://docs.aws.amazon.com/general/latest/gr/ec2-service.html

Some AWS CLI Commands
| aws ec2 describe-regions
| aws ec2 describe-regions --all-regions
| aws ec2 describe-availability-zones --region region-name
| aws ec2 describe-availability-zones --all-availability-zones

Powershell
| Get-EC2Region
| Get-EC2AvailabilityZone -Region region-name


Set a defautl region:
- Linux: AWS_DEFAULT_REGION environment variable
- Windows: Set-AWSDefaultRegion

command line options:
- Linux: --region
- Windows: -Region

You must contact AWS Support to disable a Local Zone

Migrating an instance to another Availability Zone
- Create an AMI from the original instance
- Launch an instance in the new Availability Zone
- Update the configuration of the new instance

To preserve the private IPv4 address of the instance:
- delete the subnet in the current Availability Zone
- then create a subnet in the new Availability Zone with the same IPv4 address range as the original subnet

If the original instance is a Reserved Instance, change the Availability Zone for your reservation.

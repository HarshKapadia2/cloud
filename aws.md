# AWS

- AWS: Amazon Web Services

## Global Infrastructure

- There are various regions around the world (around 25) and every region has multiple availability zones (AZs).
- Every region is isolated from other regions and every AZ is isolated from the other AZs in that regios.
- Each AZ can span over multiple data centers, but no AZ shares data centers.
- [AWS global infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)

## AWS Pricing

- [AWS pricing](https://aws.amazon.com/pricing/)
- [AWS pricing calculator](https://calculator.aws/)
- Billing alarm uses Amazon CloudWatch and Amazon SNS.

## AWS IAM

- IAM = Identity and Access Management
- IAM Policy is used to define permissions for users.
- Root account (log in with e-mail ID) has all privileges.
  - Not recommeded for regular use. Use an IAM User for daily use.
- IAM User represents users or services.
- IAM Group allows the application of an IAM Policy to a group of users.
  - It is better to assign policies to groups and the add users to groups rather than assigning policies to users individually.
- IAM Role can be assumed by a service and get the permissions provided by the policy and delegate certain things.
- [AWS IAM](https://aws.amazon.com/iam/)

## Amazon VPC

- Prerequisite: CIDR
  - [IPv4, CIDR, NAT and VPC subnets](https://www.youtube.com/watch?v=z07HTSzzp3o)

    <img src="https://user-images.githubusercontent.com/50140864/116966289-6fdd9d80-accd-11eb-9abf-e98c0d834c60.png" width="50%" />
  
  - [Understanding CIDR Ranges and dividing networks](https://www.youtube.com/watch?v=MmA0-978fSk)
  - [IP Subnetting from CIDR Notations](https://www.youtube.com/watch?v=POPoAjWFkGg)
  - Imp terms: Subnet mask, network ID, host ID, broadcast ID, 0.0.0.0/0, ::/0, gateway, router
  - Private IP address ranges:
    - For class A: 10.0.0.0/8 (10.0.0.0 to 10.255.255.255)
    - For class B: 172.16.0.0/12 (172.16.0.0 to 172.31.255.255)
    - For class C: 192.168.0.0/16 (192.168.0.0 to 192.168.255.255)

- VPC = Virtual Private Cloud
- Logically isolated portion of the AWS cloud within a region.

<img src="https://user-images.githubusercontent.com/50140864/116804325-76d4a680-ab3b-11eb-803b-84a9505f1f7b.png" width="50%" />

- Route tables are used by routers to communicate within the VPC and with the internet gateway (igw) to communitcate with the outside world.

  <img src="https://user-images.githubusercontent.com/50140864/116804645-fd8a8300-ab3d-11eb-94b2-540b860b46cf.png" />

- Services in the public subnet get a public IP address and can directly access the internet gateway. Direct access is not possible with private subnets.
- Default no. of subnets = no. of AZs in a region
- Tenancy is multi-tenancy (default/shared) and the pricing is more for a dedicated space.
- VPC -> subnets -> route tables -> internet gateway (if public facing)
- **Security group** affects instances of resources (eg: Amazon EC2) in the subnet and **NACLs (Network Access Control Lists)** affect the entire subnet. Both are responsible for allowing or disallowing certain network traffic based on rules.
  - So instance to instance talking within a subnet will be governed by a security group, but not by a NACL. NACL is only concerned with subnet to subnet or subnet to public communication.

  <br />
  <img src="https://user-images.githubusercontent.com/50140864/117050117-9e419400-ad32-11eb-81b2-23ddc9a33157.png" width="60%" />

- **Security groups** are stateful firewalls while **NACLs** are stateless firewalls.
  - Stateful firewalls send outbound traffic implicitly if the inbound for those IPs is allowed by a rule. A stateless firewall would require an explicit rule for the outbound communication even if the inbound connection was allowed by a rule.

  <br />
  <img src="https://user-images.githubusercontent.com/50140864/117053989-3e99b780-ad37-11eb-9bb8-b7723517cb1d.png" width="50%" />

- AWS public and private services

  <img src="https://user-images.githubusercontent.com/50140864/117055430-c502c900-ad38-11eb-88da-50feae59607d.png" width="60%" />

- [Amazon VPC](https://aws.amazon.com/vpc/)

## Amazon EC2

- EC2 = Elastic Compute Cloud
- Allows running virtualized servers on AWS.
- Core service at the center of everything, as it provides the compute power.

<img src="https://user-images.githubusercontent.com/50140864/117099710-82201000-ad8f-11eb-94e0-3bfd283d3ca9.png" width="50%" />

- EC2 instances in a public subnet can get a public IP address. They always have a private IP address.

  <img src="https://user-images.githubusercontent.com/50140864/117099876-f490f000-ad8f-11eb-8af5-ea102e621d00.png" width="50%" />

  - Instances within a public subnet

    <img src="https://user-images.githubusercontent.com/50140864/117100160-ac260200-ad90-11eb-865d-65574025092b.png" width="50%" />

  - Instances within a private subnet

    <img src="https://user-images.githubusercontent.com/50140864/117100257-eb545300-ad90-11eb-9e3b-e785a8d539cd.png" width="50%" />

- EC2 instance types

  <img src="https://user-images.githubusercontent.com/50140864/117100931-ac270180-ad92-11eb-89e8-f971879eca3f.png" width="50%" />

- Amazon Machine Images (AMIs)
  - [Virtualization types: HVM vs PV](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html)

- Connecting to an EC2 instance [from Windows 10 using SSH](https://www.nabh.com/blog/connecting-to-ec2-from-windows-10.html).

### Connecting different AWS services to each other

- Key pairs (access keys)
- IAM roles

  <img src="https://user-images.githubusercontent.com/50140864/117161923-f4b8dc00-addf-11eb-81eb-8ac9ea6e7c18.png" width="50%" />

### Amazon EC2 Auto Scaling

- Provides resilience, fault tolerance, availability, cost management and elasticity.
- Minimum capacity <= desired capacity <= maximum capacity
- Adding instances is called 'scaling out' and removing instances is called 'scaling in'.

<img src="https://user-images.githubusercontent.com/50140864/117202390-60fd0500-ae0b-11eb-807c-409c70c95f38.png" width="50%" />

<img src="https://user-images.githubusercontent.com/50140864/117202589-9efa2900-ae0b-11eb-8fac-f5662e85e012.png" width="50%" />

### Amazon EC2 Load Balancing

- ELB = Elastic Load Balancer

<img src="https://user-images.githubusercontent.com/50140864/117457391-cca7b500-af66-11eb-873a-a93c5d77340c.png" width="50%" />
<img src="https://user-images.githubusercontent.com/50140864/117457648-0e386000-af67-11eb-8388-c4ca0813fa29.png" width="50%" />

- Advantages of this architechture: High availability, fault tolerance and elasticity.
- Types of Load Balancers in AWS
  - Application Load Balancer (Layer 7 Load Balancer)
  - Network Load Balancer (Layer 4 Load Balancer)
  - Gateway Load Balancer
  - Classic Load Balancer (being deprecated)

- Steps
  - Create a VPC.
  - Create a security policy.
  - Create an IAM role for S3 (if used).
  - Create a Launch Template.
  - Create a [Target Group](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html). (Has the instances to be handled by the ELB.)
  - Create an IAM role.
  - Create an Auto-Scaling Group.

- What can be done is that the security group (SG) for the EC2 instance can only allow inbound traffic from the SG of the ELB. The SG of the ELB can then be allowed to be contacted by anyone on the internet for public access.
  - In such a scenario, if the link to the final app does not work (no error, but just doesn't load completely), check the ELB SG and check if it allows HTTP or HTTPS traffic from everywhere (public, i.e., 0.0.0.0/0 or ::/0).

## Amazon Storage Services

- Three types of storage
  - Amazon EBS: Block storage
  - Amazon EFS: File storage (Linux only)
  - Amazon S3: Object storage

<img src="https://user-images.githubusercontent.com/50140864/118397325-0c5e5300-b671-11eb-904a-cbbea1009304.png" width="70%" />

### Amazon EBS

- EBS = Elastic Block Store
- Block-based storage, i.e., drives/volumes.
- With EBS, one can attach volumes to EC2 instances.
- Remember to create the volume and the EC2 instance in the same AZ and subnet. Better perf, I guess?

<img src="https://user-images.githubusercontent.com/50140864/118397454-acb47780-b671-11eb-8252-fe6d2522faa0.png" width="50%" />
<img src="https://user-images.githubusercontent.com/50140864/118397523-0026c580-b672-11eb-9b52-7e49a15cead4.png" width="60%" />

- IOPS: Input Output Operations Per Second
- [RDP client](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/connecting_to_windows_instance.html#rdp-prereqs)

<img src="https://user-images.githubusercontent.com/50140864/118402018-b1832680-b685-11eb-960a-a6a459fc9a90.png" width="60%" />

#### Amazon EBS Snapshots

- EBS Snapshots are built-in volume backups.
- Snapshots can be used to back up a volume and to use its data in another AZ in a new volume.

<img src="https://user-images.githubusercontent.com/50140864/118402180-7503fa80-b686-11eb-9986-062e93c7242e.png" width="60%" />

### Amazon EFS

- EFS = Elastic File System
- File-based storage system.
- EFS can only be used with Linux and not with Windows.

<img src="https://user-images.githubusercontent.com/50140864/118404028-e182f780-b68e-11eb-8bdb-6b24ac5b3377.png" width="50%" />

### Amazon S3

- S3 = Simple Storage Service
- Object-based storage system. (Any file type is accepted, for e.g., spreadsheets, images, videos, etc.)
- It supports versioning. Deleted files or previous versions of a file can be restored, unless the saved history itself is deleted.
- The bucket needs to be empty (with) before it can be deleted.
- Public access needs to be defined at bucket level and individual object levels as well.
- Files can be uploaded from the AWS CLI as well.

<img src="https://user-images.githubusercontent.com/50140864/118412773-80bce480-b6b9-11eb-8c99-28f61156edee.png" width="50%" />

## AWS Databases

- Relational (SQL) DB: Amazon RDS
- Non-relational (NoSQL) DB: Amazon DynamoDB

### Amazon RDS

- RDS = Relational Database Service
- Engines supported
  - Amazon Aurora
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - PostgreSQL
- RDS runs on EC2 instances and the instances can be changed as and when required, at the cost of the DB temporarily going offline.
- Managed relational DB service, so it automatically handles a lot of things for the developer, like backups. Scalability, perf gains and multi-AZ fail-over for high availability and disaster recovery are also some features provided. It's difficult to do it all by oneseld.

  <img src="https://user-images.githubusercontent.com/50140864/118461519-61ef3a00-b71b-11eb-987d-798ebd0a7de2.png" width="50%" />
  <img src="https://user-images.githubusercontent.com/50140864/118462477-57817000-b71c-11eb-901c-cc870f2cb135.png" width="70%" />

### Amazon DynamoDB

- Non-relational (NoSQL) DB.

<img src="https://user-images.githubusercontent.com/50140864/118514079-e0ff6500-b751-11eb-8dc6-550cb6a0277c.png" width="50%" />

- DynamoDB is made up of
  - Tables
  - Items (rows)
  - Attributes (values) (Red box in the picture below.)

  <br />
  <img src="https://user-images.githubusercontent.com/50140864/118529704-71917180-b761-11eb-8d97-284a204567f1.png" width="50%" />

## Automation on AWS

- AWS CloudFormation
- AWS Elastic Beanstalk (PaaS)

### AWS CloudFormation

- Helps deploying intrastructure (infra) as code.
- Enables automatic infrastructure deployment on AWS through code in template files in JSON or YAML (YML) formats.
- Anything from deploying VPCs, subnet configs, DBs, etc on AWS.
- Code view 👇

  <img src="https://user-images.githubusercontent.com/50140864/119312038-74272600-bc8f-11eb-8d2b-7ce4c496a5cb.png" width="50%" />

- Graphic view of the code provided by AWS CloudFormation Designer 👇

  <img src="https://user-images.githubusercontent.com/50140864/119312240-bc464880-bc8f-11eb-9bfa-d86e2f1fb21c.png" width="50%" />

- Create stacks and upload templates.
- On deleteing a stack, it rolls back the deployed infra.
  - Even then, make sure to check that all resources are deleted, because certain modifications to the infra might lead to some infra not being rolled back (stopped).

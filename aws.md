# AWS

## Global Infrastructure

- There are various regions around the world (around 25) and every region has multiple availability zones (AZs).
- Every region is isolated from other regions and every AZ is isolated from the other AZs in that regios.
- Each AZ can span over multiple data centers, but no AZ shares data centers.
- [AWS global infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)

## AWS Pricing

- [AWS pricing](https://aws.amazon.com/pricing/)
- [AWS pricing calculator](https://calculator.aws/)

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
- Security group affects instances of resources (eg: Amazon EC2) in the subnet and NACLs (Network Access Control Lists) affect the entire subnet. Both are responsible for allowing or disallowing certain network traffic based on rules.
  - So instance to instance talking within a subnet will be governed by a security group, but not by a NACL. NACL is only concerned with subnet to subnet or subnet to public communication.

  <br />
  <img src="https://user-images.githubusercontent.com/50140864/117050117-9e419400-ad32-11eb-81b2-23ddc9a33157.png" width="60%" />

- Security groups are stateful firewalls while NACLs are stateless firewalls.
  - Stateful firewalls send outbound traffic implicitly if the inbound for those IPs is allowed by a rule. A stateless firewall would require an explicit rule for the outbound communication even if the inbound connection was allowed by a rule.

  <br />
  <img src="https://user-images.githubusercontent.com/50140864/117053989-3e99b780-ad37-11eb-9bb8-b7723517cb1d.png" width="50%" />

- AWS public and private services

  <img src="https://user-images.githubusercontent.com/50140864/117055430-c502c900-ad38-11eb-88da-50feae59607d.png" width="60%" />

- [Amazon VPC](https://aws.amazon.com/vpc/)

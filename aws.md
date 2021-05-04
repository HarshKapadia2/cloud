# AWS

## Global Infrastructure

- There are various regions around the world (around 25) and every region has multiple availability zones (AZs).
- Every region is isolated from other regions and every AZ is isolated from the other AZs in that regios.
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
- VPC = Virtual Private Cloud
- Logically isolated portion of the AWS cloud within a region.

<img src="https://user-images.githubusercontent.com/50140864/116804325-76d4a680-ab3b-11eb-803b-84a9505f1f7b.png" width="50%" />

- Route tables are used by routers to communicate within the VPC and with the internet gateway (igw) to communitcate with the outside world.

<img src="https://user-images.githubusercontent.com/50140864/116804645-fd8a8300-ab3d-11eb-94b2-540b860b46cf.png" />

- Services in the public subnet get a public IP address and can directly access the internet gateway. Direct access is not possible with private subnets.
- Default no. of subnets = no. of AZs in a region
- Tenancy is multi-tenancy (default/shared) and the pricing is more for a dedicated space.
- [Amazon VPC](https://aws.amazon.com/vpc/)

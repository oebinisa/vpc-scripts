# AWS CloudFormation Scripts

# 1. Creating a VPC Using CloudFormation:

- Public and Private Subnets
- In 2 different AZs
  - Script: vpc.yaml
  - Architecture Diagram: vpc-with-public-and-private-subnets.jpg

VPC Creation Steps - CloudFormation Resources Section:

1. Create VPC
2. Create Internet Gateway
3. Attach the Internet Gateway to the VPC
4. Create the Public Subnets
5. Create Public Route Tables
6. Add Public Route to the Public Route Table
7. Associate the Public Subnets with the Public Route Table
8. Create the Private Subnets
9. Create the Security Groups
   1. Application Load Balancer
   2. SSH
   3. EC2
   4. RDS

# 2. Creating a Nat Gateway Using CloudFormation:

- Public and Private Subnets

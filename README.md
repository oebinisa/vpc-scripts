# AWS CloudFormation Scripts

# 1. Creating a VPC Using CloudFormation:

- Public and Private Subnets
- In 2 different AZs
  - Script: vpc.yaml
  - Architecture Diagram: vpc-with-public-and-private-subnets.jpg

VPC Creation Steps:

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

Warning:
Running a NAT Gateway all the time is going to be very expensive. AWS charge per hour for a NAT Gateway.
The purpose for the NAT Gateways in this video is for updates and/or patches, therefore only launch your NAT Gateway stack when you are performing those actions, otherwise keep this stack off!

NB: This will utilize the VPC Stack from (1) above.

Creation Steps:

1. Allocate Elastic IP Address
2. Create Nat Gateway in each Public Subnets
3. Create a Private Route Table
4. Add a route to point internet-bound traffic to Nat Gateway
5. Associate Private Subnets with Private Route Table

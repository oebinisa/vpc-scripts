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

- Dependencies: VPC stack - (1) above

Creation Steps:

1. Allocate Elastic IP Address
2. Create Nat Gateway in each Public Subnets
3. Create a Private Route Table
4. Add a route to point internet-bound traffic to Nat Gateway
5. Associate Private Subnets with Private Route Table

# 3. Creating an RDS Database Using CloudFormation

- This template creates an RDS database with MySQL Engine
- Dependencies: VPC stack - (1) above
- It takes its outputs from (1) VPC Creation above
- After uploading the stack to the CloudFormation console, enter the following values into the following fields:
  - Specify stack details:
    - Stack name: rds
    - Export VPC Stack Name: vpc

# 4. Creating an ALB Using CloudFormation

- This template creates an Application Load Balancer
- Dependencies: VPC stack - (1) above
- After uploading the stack to the CloudFormation console, enter the following values into the following fields:
  - Specify stack details:
    - Stack name: alb
  - Parameters:
    - Certificate Arn: Generate and copy/paste your site/project ARN from AWS Certificate Manager
    - Export VPC Stack Name: vpc

# 5. Add EC2 Instances to ALB Target Group Using CloudFormation

- This is a follow up on (4) above - Creating an ALB Using CloudFormation
- This demonstrates how to add single EC2 instance to the Target Group of the ALB (Application Load Balancer)
- Two EC2 instances were added to the Target Group here
- Dependencies: VPC stack - (1) above
- After uploading the stack to the CloudFormation console, enter the following values into the following fields:
  - Specify stack details:
    - Stack name: alb
  - Parameters:
    - Certificate Arn: Generate and copy/paste your site/project ARN from AWS Certificate Manager
    - Export VPC Stack Name: vpc
    - EC2 Parameters: Enter AmazonImageID
    - KeyName: Select your pre-created EC2 KeyPair

Creation Steps:

1. Create the EC2 instance you intend to add to the ALB Target Group
   Template: ec2-reference.yaml
2. Merge the script with alb.yaml from (4) above
3. Expand the alb.yaml to allow for creation of 2 EC2 instances

# 6. Creating an Auto Scaling Group (ASG) Using CloudFormation

- This template creates an Auto Scaling Group using CloudFormation
- Dependencies:
  - VPC stack - (1) above
  - ALB - (4) above
  - ALB Target Group - (5) above
- After uploading the stack to the CloudFormation console, enter the following values into the following fields:
  - Specify stack details:
    - Stack name: asg
  - Parameters:
    - Export VPC Stack Name: vpc
    - Export ALB Stack Name: alb
    - Email Address: Enter Operator Email Address
    - Image ID: Enter AmazonImageID
    - EC2 KeyPair: Select your pre-created EC2 KeyPair

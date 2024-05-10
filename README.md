# AWS CloudFormation Template

## Overview

This CloudFormation template is designed for deploying infrastructure on AWS for Maria Park's final project. It sets up a virtual private cloud (VPC) with public and private subnets across multiple availability zones. It also creates an internet-facing application load balancer (ALB) with auto-scaling groups for high availability and scalability. Instances launched within the VPC serve web content via Apache HTTP Server and are tagged appropriately.

## Parameters

- `VPCCIDR`: The CIDR block for the VPC. Default: 17.0.0.0/16
- `PublicSubnet1CIDR and PublicSubnet2CIDR`: CIDR blocks for the public subnets in different availability zones. Default: 17.0.1.0/24 and 17.0.2.0/24 respectively.
- `PrivateSubnet1CIDR and PrivateSubnet2CIDR`: CIDR blocks for the private subnets in different availability zones. Default: 17.0.3.0/24 and 17.0.4.0/24 respectively.
- `MyInstanceType`: Instance type for launched instances. Allowed values: t2.micro, t3.micro. Default: t2.micro.
- `ProjectTags1 and ProjectTags2`: Tags for the resources. Default: Owner=Maria and Project=Final.

## Resources

### VPC and Subnets
- Creates a VPC with DNS support and hostnames enabled.
- Sets up public and private subnets in different availability zones within the VPC.
- Associates route tables with subnets and configures internet and NAT gateways for public and private subnets respectively.

### Instances, Load Balancer and Autoscaling groups
- Launches instances using a launch template with user data to install and configure Apache HTTP Server.
- Configures an application load balancer (ALB) with listeners and target groups for distributing traffic to instances.
- Sets up auto-scaling groups for scaling instances based on demand.

### Security group
- Defines security groups allowing SSH and HTTP traffic.

## Outputs
- `ALBDNSName`: The DNS name for the load balancer.
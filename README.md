
# Terraform Infrastructure Assignment 

#### GOAL 

The goal of this assignment is to design and implement the infrastructure for your individual tool using Terraform IaC (Infrastructure as Code). You will follow best practices, manage the Terraform state file in an S3 bucket, and ensure consistent provider versioning throughout your code.





# Steps to Complete the Assignment


- ## Implement the Infrastructure with Terraform
- ### Write Terraform code to:
- Create a VPC with DNS support and hostnames enabled.
- Define public and private subnets across two availability zones.
- Attach an internet gateway for public subnets.
  Configure route tables for public and private traffic.
- Create a security group for public EC2 instances with rules for SSH and HTTP access.
- Launch EC2 instances in public subnets with appropriate AMI and key pair.
# Let's put it into practice...🚀



## 1. Creating the infrastructure using code


### Terraform AWS VPC Setup

This repository contains Terraform code to provision a Virtual Private Cloud (VPC) in AWS with public and private subnets, an internet gateway, and EC2 instances.

## Requirements

- [Terraform](https://www.terraform.io/downloads.html) v1.5.0 or later
- AWS account credentials with necessary permissions
- [AWS CLI](https://aws.amazon.com/cli/) (optional, but recommended)
- SSH key pair (`mykey.pem` or update the code to use your key name)

## Key Reference Table

| Reference | Description                        |
|-----------|------------------------------------|
| `ami-12345` | Example AMI ID for EC2 instances. |
| `mykey.pem` | Name of your AWS key pair.        |
| `us-east-1` | AWS region for deployment.        |


## Components

### VPC
- A single VPC with CIDR block `10.0.0.0/16`
- DNS support and DNS hostname enabled

### Subnets
- **Public Subnet 1:** `10.0.1.0/24` in availability zone `us-east-1a`
- **Public Subnet 2:** `10.0.2.0/24` in availability zone `us-east-1b`
- **Private Subnet 1:** `10.0.3.0/24` in availability zone `us-east-1a`
- **Private Subnet 2:** `10.0.4.0/24` in availability zone `us-east-1b`

### Internet Gateway
- An Internet Gateway is attached to the VPC for internet access for public subnets.

### Route Tables
- A public route table with routes to the Internet Gateway
- Public subnets associated with the public route table

### Security Groups
- A security group to allow:
  - SSH (port 22) access from anywhere
  - HTTP (port 80) access from anywhere
  - All outbound traffic

### EC2 Instances
- Two EC2 instances in public subnets:
  - **Instance 1:** Located in `Public Subnet 1`
  - **Instance 2:** Located in `Public Subnet 2`
  - Instance type: `t2.micro`
  - AMIs: Replace with valid AMI IDs
  - SSH key: `mykey.pem` (Update to your key name if different)

## How to Use

### 1. Clone the Repository
```bash
git clone <repository-url>
cd <repository-directory>
```

### 2. Configure Backend
Update the `backend` section in the `terraform` block to match your S3 bucket configuration:

```hcl
backend "s3" {
  bucket = "<your-s3-bucket-name>"
  key    = "<your-backend-key>"
  region = "<your-region>"
}
```

### 3. Initialize Terraform
Run the following command to initialize Terraform and download the necessary provider plugins:
```bash
terraform init
```

### 4. Review the Plan
Review the changes Terraform will apply:
```bash
terraform plan
```

### 5. Apply the Configuration
Apply the Terraform configuration to create the resources:
```bash
terraform apply
```
Confirm with `yes` when prompted.

### 6. Clean Up
To remove all resources created by Terraform:
```bash
terraform destroy
```
Confirm with `yes` when prompted.



## Notes 💬

- *Ensure the specified AMI IDs in the EC2 instances are valid for your region.*
- *Replace `mykey.pem` with the name of your existing AWS key pair.*
- *Update the `region` in the provider block and availability zones as per your requirements.*

## Environment Setup References
| Reference   | Description                                                |
|-------------|------------------------------------------------------------|
| `aws provider` | Check for Provider for infra. See [Use Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs). |
| `AWS resources` | Check for AWS resources  [AWS Resources](https://registry.terraform.io/providers/hashicorp/aws/2.43.0/docs). |


## Authors

- [@Durgeshsharma](https://github.com/duggu7055/assignment-1/tree/main)


AWS EKS Infrastructure Documentation

Overview
This Terraform configuration sets up a production-ready Amazon EKS cluster with associated networking and security components. The infrastructure is designed to be highly available across two availability zones.

Infrastructure Components

VPC and Networking
- VPC with CIDR block 10.0.0.0/16
- 2 public subnets (10.0.1.0/24, 10.0.2.0/24)
- 2 private subnets (10.0.3.0/24, 10.0.4.0/24)
- NAT Gateways in each public subnet
- Internet Gateway for public internet access
- Separate route tables for public and private subnets

EKS Cluster
- Kubernetes version: 1.30
- Private endpoint access enabled
- Public endpoint access enabled
- Node group configuration:
  - Instance type: t3.medium
  - Min nodes: 2
  - Max nodes: 4
  - Desired nodes: 2

IAM Configuration
- EKS cluster role with required policies
- Node group IAM role with necessary permissions
- OIDC provider for service account integration
- ALB Ingress Controller IAM role and policies

Usage

1. Configure AWS credentials:
export AWS_ACCESS_KEY_ID="your_access_key"
export AWS_SECRET_ACCESS_KEY="your_secret_key"

2. Initialize Terraform:
terraform init

3. Review planned changes:
terraform plan

4. Apply the configuration:
terraform apply

Important Variables

Variable         Description              Default
-----------------------------------------------
aws_region      AWS region to deploy to  us-east-1
cluster_name    Name of the EKS cluster  eks
cluster_version Kubernetes version       1.30
node_instance_type EC2 instance type    t3.medium
vpc_cidr        VPC CIDR block          10.0.0.0/16

Available Outputs

- vpc_id: ID of the created VPC
- cluster_endpoint: EKS cluster API endpoint
- cluster_iam_role_arn: ARN of the cluster IAM role
- cluster_oidc_issuer_url: OIDC provider URL
- public_subnet_ids: List of public subnet IDs
- private_subnet_ids: List of private subnet IDs
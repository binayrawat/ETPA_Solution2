# HTTPBin Kubernetes Setup

A simple Kubernetes configuration for deploying HTTPBin with both public and private access through AWS Application Load Balancers (ALB).

## Components

- **HTTPBin Deployment**: Runs 2 replicas of the HTTPBin service
- **Kubernetes Service**: Exposes HTTPBin pods internally
- **Public Ingress**: Provides internet-facing access to `/get` endpoint
- **Private Ingress**: Internal access to `/post` endpoint (VPC only)

## Prerequisites

- Kubernetes cluster on AWS
- AWS Load Balancer Controller installed
- Appropriate VPC with public and private subnets

## Quick Start

Deploy the components in the following order: 
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml

Deploy AWS ALB Ingress controller 
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=eks \
  --set serviceAccount.create=true \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set serviceAccount.annotations."eks\.amazonaws\.com/role-arn"=<arn:aws:iam::422248601475:role/eks-alb-ingress-controller> \
  --set region=us-east-1 \
  --set vpcId=<vpc-008db9330b2061942>

kubectl apply -f kubernetes/pub-ingress.yaml
kubectl apply -f kubernetes/pvt-ingress.yaml


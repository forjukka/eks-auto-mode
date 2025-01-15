# Amazon EKS Auto Mode demo

This repo aims to provide a super simple, but highly impressive demo of EKS Auto Mode that was released at AWS re:Invent 2024.

## Instructions

1. Install and setup AWS CLI and your credentials
2. Install eksctl from your preferred source
3. eksctl create cluster --name=CLUSTER_NAME --version 1.30 --enable-auto-mode # nodegroup and addons are not needed!
4. kubectl apply -f nginx-demo.yaml
5. NGINX_DEMO=$(kubectl get ingress nginx-ingress -n nginx-demo -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
6. curl $NGINX_DEMO # run this after a couple of minutes when ALB has finished provisioning.
7. eksctl delete cluster --name=CLUSTER_NAME # don't forget the cluster running after you're done!

## What's the beauty here?

- We provioned a production grade EKS Auto Mode cluster and didn't need to configure any node groups, addons, etc.
- The cluster starts scaled to zero, but when we provision the nginx-demo, we see a worker node appear in seconds.
- ALB and EBS volume for the application are provisioned and configured automatically.
- When we update the control plane to a newer version, then we will see all worker nodes and addons upgraded automatically.
- Security updates would also be applied automatically to the nodes.
- In short, EKS Auto Mode makes Kubernetes easy!

## Terraform support

See "EKS Auto Mode" chapter in here: https://registry.terraform.io/modules/terraform-aws-modules/eks/aws/latest

## AWS CDK support

EKS Auto Mode is not yet supported in the L2 construct for EKS cluster (1/2025).

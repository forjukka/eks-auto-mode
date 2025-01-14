# EKS Auto Mode demo

This repo aims to provide a super simple, but highly impressive demo of EKS Auto Mode that was released at AWS re:Invent 2024.

## Instructions

1. Setup AWS CLI and your credentials
2. eksctl create cluster --name=<cluster-name> --version 1.30 --enable-auto-mode # nodegroup and addons are not needed!
3. kubectl apply -f nginx-demo.yaml
4. NGINX_DEMO=$(kubectl get ingress nginx-ingress -n nginx-demo -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
5. curl $NGINX_DEMO # run this after a couple of minutes when ALB has finished provisioning.

# What's the beauty here?

- We provioned EKS cluster with Auto Mode and didn't need to configure node groups, addons, etc.
- The cluster starts scaled to zero, but when we provision the nginx-demo, we see worker node provisioned automatically.
- Also the ALB and EBS volume are provisioned automatically.
- When we update the control plane to a newer version, then we will see worker nodes upgraded automatically after certain delay.
- The same will happen with security updates to the underlaying Bottlerocket AMI when a new version is released.

# Terraform support

See "EKS Auto Mode" chapter in here: https://registry.terraform.io/modules/terraform-aws-modules/eks/aws/latest

# AWS CDK support

EKS Auto Mode is not yet supported in the L2 construct for EKS cluster.
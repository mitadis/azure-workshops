# AKS Impossible Problems

## 1. Infrastructure preparation
### Create resources through AzCLI/Powershell/Bicep/ARM Template or Terraform automation
- 2x Virtual Network (Application and Hub)
- 1x Azure Firewall
    - Deployed to Hub Virtual Network
- 1x Route Table
- 1x VNET Peering
    - Between Application Network and Hub Network
- 1x Network Security Group
- 1x NAT Gateway
- 1x Dedicated Managed Identity for Kubernetes Service
- 1x Log Analytics Workspace with Daily Data Quota of 1 GB
- Minimal permissions for Kubernetes Managed Identity
- 1x Azure Container Registry
- 1x Azure Kubernetes Cluster
    - 2x Node Pool - 1 for system, 1 for applications
    - Custom network profile using kubenet network plugin and addressing statically defined by you
    - Use User Assigned Managed Identity
    - Kubelet identity should be the same as AKS Identity
    - Integrated with Application Virtual Network
    - ALL Traffic to the Internet from AKS should go through Azure Firewall in the Hub Network
    - AKS Node Resource Group Name should be defined by you (NOT GENERATED AUTOMATICALLY)
    - Integrated with Azure Container Registry using Managed Identity
    - Deploy 1 chosen Application to AKS from image in ACR

## 2. Incorrect AKS Node Resource Group Removal Troubleshooting
### Steps to get to the problem:
1. Remove from the Azure Portal the whole Resource Group with AKS Node (the resource group that's automatically created during AKS deployment)
2. After it's finished try to remove AKS Cluster
3. Try to fix this state :)
4. If you succeed write down all steps required to fix it

## 3. Incorrect Managed Identity Removal Troubleshooting
1. Remove from the Azure Portal Managed Identity that's used by Azure Kubernetes Cluster
2. After it's finished try to:
    - stop the cluster
    - start the cluster
    - update application image to newer version and apply it on the cluster
3. Try to fix this state :)
4. If you succeed write down all steps required to fix it

## Summary:
- Prepare Architecture Diagram describing your solution
- The application code & Infrastructure As Code should be stored in your Git Repository
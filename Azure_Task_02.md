# Azure dedicated Infrastructure as Code (IaC) environment
## Deploy resources using:
1. Azure Resource Manager (ARM) Templates:
   - there should be 2 files:
     - deployment:
       - parameters definition (parameter name, type)
       - variables definition (name, type)
       - resources deployment
     - parameters:
       - parameters deployment (values)
   - docs: https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview
2. Bicep:
	- there should be 2 files:
      - deployment:
          - parameters definition (name, type)
          - variables definition (name, type)
          - resources deployment
      - parameters:
          - parameters deployment (values)
   - docs: https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep

## Resources to be deployed:
- 1x Virtual Machine [Jumpbox] with:
	- Windows Server 2022
	- sizing - no more than 2 vCPU & 8 GB RAM
	- all necessary resources (Network Interface Configuration, OS Disk, etc)
- 2x Virtual Machines [Web Server] with:
	- Ubuntu Server 22.04 LTS
	- sizing - no more than 1 vCPU & 4 GB RAM
	- login allowed only with SSH Key
	- all necessary resources (Network Interface Configuration, OS Disk, etc)
    - First VM with nginx, Second VM with apache (deploy it however you want - script, by hand etc.)
- 1x Virtual Network
- 2x Subnets (first for Jumpbox, second for Web Servers)
- 2x Network Security Groups (for each Subnet)
- 1x Public IP Address

## Limitations
- try to stick to a naming convention that is already in use f.e. RG-NAME, VNET-NAME, VMNAME01 etc. You can find recommended abbreviations here: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations
- try to only use official documentation and **DO NOT** use json <-> bicep translation tools
- Jumpbox VM should be accessible:
	- from the Public Network
	- only on port 3389, TCP Protocol
	- only from your Public IP Address
- Web-server VMs should be accessible:
	- only from Jumpbox Subnet
	- only on port 22 & 80, TCP Protocol
	- only from the Subnet of the first VM
- Web Servers should not be able to connect to each other

## Tasks
1. Deploy resources through each method and check if the above environment works correctly:
   - Connect to 1st VM through RDP on port 3389 through its Public IP Address
   - Go to http://_1st_web_server_private_ip and check if there is a nginx default page available
   - Go to http://_2st_web_server_private_ip and check if there is a apache default page available
   - Connect to 1st Web Server through SSH on port 22 and check if you can connect to 2nd Web Server on port 22 or 80
   - After successful connections remove the environment
2. Create 2 Architecture Diagrams of this environment:
	- Networking
    - Resources
3. Create a table summarizing differences between deployment methods
# Virtual Machines in Three Flavours
## Deploy resources using:
1. Azure Portal
2. Script: Az PowerShell Module in PowerShell 7 (docs: https://learn.microsoft.com/en-us/powershell/module/?view=azps-9.1.0)
3. Script: AZ CLI (docs: https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)

## Resources to be deployed:
- 2x Virtual Machines with:
	- Rocky Linux 9 from The Rocky Enterprise Software Foundation Inc provider (free tier)
	- sizing - no more than 1 vCPU & 4 GB RAM
	- login allowed only with SSH Key
	- all necessary resources (Network Interface Configuration, OS Disk, etc)
- 1x Virtual Network
- 2x Subnets (for each VM)
- 2x Network Security Groups (for each Subnet)
- 1x Public IP Address

## Limitations
- try to stick to a naming convention that is already in use f.e. RG-NAME, VNET-NAME, VMNAME01 etc. You can find recommended abbreviations here: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations
- try to only use official documentation
- 1st VM should be accessible:
	- from the Public Network
	- only on port 22, TCP Protocol
	- only from your Public IP Address
- 2nd VM should be accessible:
	- only from Private Virtual Network
	- only on port 22, TCP Protocol
	- only from the Subnet of the first VM

## Tasks
1. Deploy resources through each method and check if the above environment works correctly:
   - Connect to 1st VM through SSH on port 22 through its Public IP Address
   - On 1st VM copy and paste private SSH key to 2nd VM
   - On 1st VM connect to 2nd VM through SSH on port 22 through its Private IP Address
   - After successful connections remove the environment from Azure Portal (or extra challenge - remove through AZ CLI or PowerShell)
2. Create a Architecture Diagram of this environment in draw.io or other tool (Visio, Lucidcharts, etc.)
3. Create a table summarizing differences between deployment methods
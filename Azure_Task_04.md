# Azure App Services

## 1. Infrastructure preparation
### Create resources however you want (Azure Portal, AzCLI, AzPowerShell Module, Bicep, ARM Template, Terraform):
- Virtual Network (/24)
- 4x Subnets (/26)
- 2x App Service Plan (1 for Web Apps, 1 for Function Apps)
- 1x Application Insights
- 1x Jumpbox VM:
	- Operating System - whatever suits you
	- with accessibility through Application Gateway's Public IP)
- 1x Key Vault
- 1x Storage Account
- 1x Application Gateway:
	- WAFv2 tier
	- with Public IP
	- with Private IP
	- Routing from Public IP to Jumpbox VM
	- Routing from Private IP to Web Apps

## 2. Deploy a Python (Django or Flask) Web App to Azure App Service
### Requirements:
- Web Application in Python that contains:
	- "Hello World From _YourInitials_"
	- Logo of your choice
	- Reads a CSV File from the user and presents it as a table (prepare or get a file that suits you)
	- Creates a chart from the data in the CSV File (create at least 2 lines on a chart, choose whichever column from CSV that suits you)
- The app should:
	- be accessible only through Application Gateway's Private IP
	- be https-only and use SSL Certificate generated through Lets-Encrypt
	- the Certificate should be stored in Key Vault and used by app through Key Vault
	- be integrated with Application Insights through Key & Connection String in Azure Key Vault which is retrieved through Configuration tab in web app
	- be integrated with Virtual Network

## 3. Azure Function Application
### Requirements:
- Function App in Python that:
	- performs availability test against:
		- ICMP: ping to Jumpbox Private IP address
		- RDP: 3389 & Jumpbox Private IP address
		- HTTPS: 443 & Application Gateway's Private IP Address
	- saves result for each of above tests to Application Insights
	- is triggered every 30 seconds

## Summary:
- Prepare Architecture Diagram describing your solution
- The application code & Infrastructure As Code should be stored in your Azure DevOps Repository
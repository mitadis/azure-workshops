# Cost optimization & a friend from the past

## 1. AKS Cluster scheduled shutdown/start-up

### Create automation that changes state of your AKS cluster:
- turns off every day after work
- turns it on on weekdays
- ensures it's off on weekends

Use whatever you want:
- Task Scheduler,
- Azure Function,
- Azure Logic Apps,
- APIs,
- something to impress others :D

but remember to minimize costs :)

## 2. AzCLI without shortcuts

### Deploy resources using AzCLI:
- 1x Virtual Machine [Windows] with:
	- Windows Server 2022 Gen 2
	- sizing - no more than 2 vCPU & 8 GB RAM
	- all necessary resources (Network Interface Configuration, OS Disk, etc)
    - static private IP: 172.18.1.150
- 2x Virtual Machines [Linux] with:
	- Ubuntu Server 22.04 LTS Gen 2
	- sizing - no more than 1 vCPU & 4 GB RAM
	- login allowed only with SSH Key
	- all necessary resources (Network Interface Configuration, OS Disk, etc)
    - First VM with nginx, Second VM with Grafana (https://grafana.com/)
    - static private IPs: nginx (172.18.1.200), grafana (172.18.1.210)
- 1x Virtual Network (172.18.1.128/25)
- 2x Subnets (first for Windows (/26), second for Linux (/26))
- 2x Network Security Groups (for each Subnet)

### Limitations
- Treat Windows as Jumpbox
- Windows NIC CAN NOT be associated with Public IP. Figure out alternative way to connect to it
- Linux VM's apps should be deployed without connecting through SSH to VMs (but you can connect to nginx VM to configure reverse-proxy to Grafana)
- Windows VM should be accessible:
	- just-in-time on port 3389, TCP Protocol
- Grafana should be accessible:
	- only from Windows Subnet
	- only on port 80, TCP Protocol
	- only through nginx VM so the connection works like this: Windows VM -> Nginx VM -> Grafana VM 
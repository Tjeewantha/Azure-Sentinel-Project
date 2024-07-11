# Azure Lab Creation
### Creating Virtual Network for Lab

To create any resources in Azura, you need to have resource group which helps you to group up your deployments according to your project sections.

Let us create resource group (Cloud-Net-Res)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%281%29.png?raw=true)

Now, you can create any resources under this resources group

To create isolated environment for the lab, you need to have virtual network. When creating virtual network, you must be  careful with subnetting. Therefore, it would be better if you  pre-define how many hosts (VMs) are  going to be deployed under which subnets.

In this case,

 - Virtual Network CIDR: 10.10.10.0/24
 - Virtual Network Name: Cloud-Net
 - Subnet1: 10.10.10.0/26 (AzureFirewallSubnet)
 - Subnet2: 10.10.10.64/26 (DMZ-Sub)

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%282%29.png?raw=true)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%289%29.png?raw=true)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2810%29.png?raw=true)

### Creating virtual machine

In this project, we hope to create 2 VMs. One is for Windows and the other is for Linux.

Both creating will follow the same process but there are some unique changes to make.

When you are going to create the VMs, make sure to add them into DMZ-Sub subnet. And do not assign any public IP to them.

Both VMs Networking should look like this in review stage.
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2811%29.png?raw=true)

Once you deployed the VMs, go to the corresponding network interfaces of each VMs and change private Ip address settings from dynamic to static.

By considering the convenience to recognize the VMs, set static Ips to followings:

 - For windows – 10.10.10.70
 - For Linux – 10.10.10.80
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2828%29.png?raw=true)
Do the same configuration to Linux VM

### Deploying Azure Firewall

Azure firewall is a next-generation firewall which gives two-layer protection.

 - Network layer
 - Application layer

And it also has Network address  translation features.

To deploy Firewall, we need at least two interfaces. in this case two subnets which we have configured already.

 - AzureFirewallSubnet – 10.10.10.0/26
 - DMZ-Sub – 10.10.10.64/26

Apart from that subnet we must have public Ip address (AzureFW-Ip) to connect our Firewall to the WAN.
Here the screenshot of the Firewall creation review:
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2812%29.png?raw=true)

When you are configuring the firewall, make sure to choose  AzureFirewallSubnet as its private subnet.

### Assigning Firewall rules

Firewalls deny all traffic by default. Therefore, you need to add some rules to allow legitimate traffic you want.

As we did not config public Ips to our VMs, we will not be able to connect to them via our host machine. On the other hand, our goal is to send all traffic to VMs through the firewall.

As First rule, you must create NAT rule allowing RDP and SSH to windows and Linux, respectively. You can map those connection with Firewall public Ip so you will be able to connect to each system by just changing port number.
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2815%29.png?raw=true)

To connect windows VM, you can use your windows Remote desktop connection via RDP (3389)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2829%29.png?raw=true)

To connect Linux VM, you can use your windows terminal via SSH (22)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2830%29.png?raw=true)

In addition to that we want our VMs to connect with internet so you should allow DNS traffic from VMs to internet under network level.
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2816%29.png?raw=true)

Under application level, allow VMs to reach google or whatever target web you want to visit.
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2817%29.png?raw=true)

Even if you have configured everything  perfectly so far, you still could not connect to your VMs. It is because of route table.

### Creating route table

The route table will decide which path should traffic go through in your virtual network. In this scenario, we need to hit the traffics that comes from our VMs to Firewall and vice versa. Route table is resource you must create.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2813%29.png?raw=true)

After route was created, you should assign that into relevance subnet.  In this project, it is DMZ-Sub.
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2814%29.png?raw=true)

Now, you will be able to connect with the VMs not having any troubles.
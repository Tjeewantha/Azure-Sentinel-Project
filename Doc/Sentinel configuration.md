# Azure Sentinel Configuration
### Deploying Log analytics workspace

Log Analytic workspace is the resource manage all logs that comes from various sources in cloud. with the help of this, you will be able to query  any log entities and correlate them with other sources of logs. More importantly, Log analytic workspace is a must-have when we going to work with Azure Sentinel.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2818%29.png?raw=true)

Now you can get into Sentinel dashboard through that created workspace

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2839%29.png?raw=true)

### Ingesting VM’s logs into Sentinel


There are couple of ways to ingest Azure virtual machine’s logs into Sentinel workspace.

 - Installing azure agent manually on VMs
 - Using Azure Agent Monitor (AMA) feature

You do not need to go with first method as we do not use any on-premises  infrastructure on our project. On the other hand, Microsoft is no longer support this service near further.

Let us config Azure Monitoring Agent on our VMs.

To work with AMA, you must create Data Collection Rule (DCR) for each set of VM types. For example, if you have multiple windows VMs and Unix VMs, you should  define a CDR for each set of VM groups.

Go to Azure Monitor and create data collection rule
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2831%29.png?raw=true)


The following screenshot show how to create DCR for our Linux VM.

>Note: Before you create and deploy the DCRs, make sure to run the corresponding VMs. Because The CDR deployment will attach the Azure Monitor Agent into that VMs automatically.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2832%29.png?raw=true)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2833%29.png?raw=true)
![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2834%29.png?raw=true)

Now you have perfectly created and deployed your DCR but if you went to Sentinel  workspace to see if there are any Linux logs have been shown, you see nothing. Why? You have not yet added any data collector for Sentinel workspace. So,  let us add syslog Data connector via Content Hub.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2835%29.png?raw=true)

To get Windows Event logs into Sentinel, you must use Windows Security Event connector.

 > For Linux,
 ![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2840%29.png?raw=true)
 
 >For Windows,
  ![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2841%29.png?raw=true)

It might take some time to work connectors properly. If you have successfully connected, you will see a green bar at the corner of your connector (As you see in windows connector up here).

### Ingesting Azure Firewall logs into Sentinel

To collect logs from Azure Firewall, you need to change setting in Azure Firewall diagnostic tab.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2836%29.png?raw=true)

Once you have made those changes, install Azure Firewall connector via Sentinel Content Hub.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2837%29.png?raw=true)

Give a little time to establish connection between Azure Firewall and sentinel.

### Collecting data from other cloud entities for Sentinel


When we come to Azure cloud entities, there are plenty of thing to discuss. However, business-wise, there are few mostly used azure cloud services.

 - Azure Active Directory (Microsoft Entra ID)
 - Microsoft 365
 - Microsoft Defender
 - Azure Web Service

To collect logs that generated from these entities, you must  add required data connector config, them in a proper way.

For demonstration, let us ingest activity logs into sentinel.

Activity Logs generates from cloud resource groups. Firstly, let us  make few changes in Diagnostic settings under our resource group (LAB-Net-Res).

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2827%29.png?raw=true)

Then, you can add Azure Activity data connector via Sentinel Content Hub.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2842%29.png?raw=true)

### Connecting a Threat Intelligence server into Sentinel

Threat Intelligence will help security analysts to investigate triggered alerts with ongoing threat and trends. We are going to use Plusedive as our Threat Intelligence source.

To connect the server, you must install Threat Intelligence data connector via Sentinel Content Hub. And you need to sign in to Plusedive.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2843%29.png?raw=true)

If you expand more details of Threat Intelligence-TAXII data connector, it asks some information about your TAXII API.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2826%29.png?raw=true)

As we are doing training project and not going to buy any subscriptions for Plusedive, we can play with test data it provides.

![Vnet](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2825%29.png?raw=true)
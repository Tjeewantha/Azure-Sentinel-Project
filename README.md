# Azure sentinel Project
Azure sentinel is a cloud-native SIEM solution. I will aid for security analysts, incident responders,  security researcher to collect, correlate and investigate the logs from different sources. Not only that it also come up with other features such as Incident Management, Threat hunting,  Threat Intelligence and so on. Unlike other SIEMs, Azure sentinel have pre-built rules for anomaly detection with support of ML and query sets that can be used to do further investigation on triggered alerts.

 ### summary:

 During this project, we hope to create operation-ready Azure sentinel workspace. As this whole project is going to be covered with Azure free subscription, we may encounter some limitation in resource deployment. Therefore, The only two VMs we going to be connected into Azure sentinel.

The project diagram:
![main](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/main.png?raw=true)

### The project we have divided into two parts.

 1. [Creating private Lab environment](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Doc/Lab%20deployment.md) 
 2. [Configuring Azure sentinel](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Doc/Sentinel%20configuration.md)

Note: During this project, make sure to put  all cloud resource under one Resource group. and region


###  The sentinel dashboard looks like at the end of the project

![dashbord](https://github.com/Tjeewantha/Azure-Sentinel-Project/blob/main/Screenshots/Screenshot%20%2844%29.png?raw=true)

>Note: Azure sentinel training module will be installing at the end of the project. it ingests certain data into our sentinel so we can play around with them to gain experience in Incident response.

## Reference
https://learn.microsoft.com/en-us/training/modules/intro-to-azure-sentinel/
https://learn.microsoft.com/en-us/azure/sentinel/skill-up-resources
https://pulsedive.com/
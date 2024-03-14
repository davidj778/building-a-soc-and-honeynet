[Main Page](https://github.com/davidj778/davidj778)

# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://imgur.com/aq4Ki6P.jpg)

## Introduction

In this project, I built a small-scale honeynet within Azure and gathered log data from diverse sources into a Log Analytics workspace. This data is utilized by Microsoft Sentinel to construct attack visualizations, activate alerts, and generate incident reports. I measured security metrics in the vulnerable environment over a 24-hour period, implemented security measures to fortify the environment, conducted another 24-hour assessment, and present the findings below. The showcased metrics include:


- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://imgur.com/ypJkZ7U.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://imgur.com/HvAT9UQ.jpg)

The Azure-based mini honeynet architecture holds the following elements:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls configured to allow all traffic, and all other resources were deployed with public endpoints accessible from the internet, which made Private Endpoints unnecessary.

For the "AFTER" metrics, Network Security Groups were strengthened by blocking ALL traffic except for access from my admin workstation. Additionally, all other resources were safeguarded by their built-in firewalls, and Private Endpoints were utilized.


## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://imgur.com/ZfHEMNQ.png)<br>
![Linux Syslog Auth Failures](https://imgur.com/Wanr1BG.png)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/12pwTNv.png)<br>
![Mssql Auth Failures](https://imgur.com/G7p4UDe.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2024-03-07 15:24:43

Stop Time 2024-03-08 15:24:43

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 17465
| Syslog                   | 2382
| SecurityAlert            | 5
| SecurityIncident         | 218
| AzureNetworkAnalytics_CL | 2502

## Attack Maps Before Hardening / Security Controls

```All map queries yielded no results as there were no instances of malicious activity detected during the 24-hour period following the implementation of security enhancements.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

Start Time 2024-03-10 02:27:55

Stop Time	2024-03-11 02:27:55

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 10133
| Syslog                   | 3
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was established within Microsoft Azure, integrating various log sources into a Log Analytics workspace. Microsoft Sentinel was utilized to trigger alerts and generate incidents based on the ingested logs. Furthermore, security metrics were assessed in the vulnerable environment both before and after the implementation of security measures. Notably, the implementation of security controls resulted in a significant reduction in the number of security events and incidents, proving their effectiveness.

It is important to acknowledge that if the network resources had been extensively used by regular users, it is probable that a greater number of security events and alerts might have been generated within the 24-hour period following the deployment of the security controls.

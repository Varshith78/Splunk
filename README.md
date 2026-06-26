# Splunk Attack Detection Lab

A hands-on lab environment for simulating common network and system attacks over a local network and analysing the resulting logs using Splunk. Each module covers a specific attack technique, walks through how it is executed, and demonstrates how to detect and investigate it using Splunk's search and alerting capabilities.



## Overview

This repository documents a series of offensive security scenarios performed in a controlled lab setup. The primary goal is to understand how attacks manifest in log data and how Splunk can be used as a SIEM to detect, correlate, and investigate suspicious activity.

The lab uses a combination of Kali Linux as the attacker machine and Ubuntu as the target, with Splunk Enterprise configured to ingest logs via the Universal Forwarder.



## Setup

Before running any of the attack modules, set up Splunk and configure log forwarding from the target machine.

[Splunk Setup - Server and Universal Forwarder](Splunk_Setup.md)

This covers installing Splunk Enterprise on the monitoring machine, installing the Universal Forwarder on the target, and configuring inputs to forward system and audit logs.



## Attack Modules

### Network Attacks

| Module | Description |
|--|-|
| [ARP Spoofing](LAN_Attacks/ARP_Spoofing.md) | Poisoning the ARP cache to perform man-in-the-middle attacks on the local network and detecting the anomalous ARP traffic in Splunk |
| [Nmap SYN Port Scan](LAN_Attacks/Nmap_SYN_Port_Scan.md) | Running stealth SYN scans against the target to enumerate open ports and identifying the scan pattern through connection logs |

### Exploitation

| Module | Description |
|--|-|
| [Vsftpd Backdoor Exploit](LAN_Attacks/Vsftpd_Backdoor_Exploit.md) | Exploiting the backdoor present in vsftpd 2.3.4 to gain a root shell using metasploitable 2 since the latest versions have been patched for this exploit |
| [FTP Brute Force Attack](LAN_Attacks/Ftp_Brute_Force_Attack.md) | Performing credential brute force against an FTP service and detecting repeated failed authentication attempts |
| [SSH Brute Force Attack](LAN_Attacks/SSH_Brute_Force_Attack.md) | Brute forcing SSH login credentials and correlating failed login events in Splunk to identify the attack pattern |
| [Netcat Reverse Shell Attack](LAN_Attacks/Netcat_Reverse_Shell_Attack.md) | Establishing a reverse shell connection using Netcat after gaining access and detecting the outbound connection and shell spawning in logs |

### Persistence

| Module | Description |
|--|-|
| [Cron Job Persistence Attack](LAN_Attacks/Cron_Job_Persistence_Attack.md) | Planting a malicious cron job on the target system to maintain persistence and detecting the cron execution and associated audit events in Splunk |

### Data Exfiltration

| Module | Description |
|--|-|
| [Data Exfiltration via SCP](LAN_Attacks/Data_Exfiltration_Via_SCP.md) | Using SCP to transfer sensitive files from the compromised target to the attacker machine and identifying the exfiltration through EXECVE and SYSCALL audit log entries |

### Defense Evasion / Integrity

| Module | Description |
|--|-|
| [File Tampering Integrity Attack](LAN_Attacks/File_Tampering_Integrity_Attack.md) | Modifying system files on the target and detecting the changes through file integrity monitoring events in Splunk |



## Lab Environment
 
| Component | Role |
|-----------|------|
| Kali Linux | Attacker machine |
| Ubuntu | Target machine |
|Metasploitable 2 | Target Machine (Vsftpd 2.3.4 Exploit) |
| Splunk Enterprise | SIEM / log analysis |
| Splunk Universal Forwarder | Log collection agent on target |
 
Log sources monitored include `/var/log/auth.log`, `/var/log/audit/audit.log`, `/var/log/syslog`, and FTP/SSH service logs.



## Prerequisites

- A local network or virtual network connecting the attacker and target machines
- Splunk Enterprise installed and accessible on the monitoring machine (Windows was used in this setup) 
- Universal Forwarder configured on the target and forwarding logs to Splunk


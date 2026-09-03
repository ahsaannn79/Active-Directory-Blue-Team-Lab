# 🛡️ Active Directory Blue Team Home Lab

A hands-on Active Directory security lab designed to explore enterprise identity infrastructure, Windows security telemetry, attack simulation, SIEM monitoring, and detection engineering.

The project follows a complete Blue Team workflow:

**Build → Monitor → Attack → Detect → Investigate → Mitigate**
## 📖 Project Overview

This project is a self-built Active Directory Blue Team home lab created to gain practical experience with enterprise Windows environments, centralized security monitoring, attack simulation, and detection engineering.

The lab was built as an isolated virtual environment where Active Directory attacks could be safely simulated while collecting and analyzing the resulting security telemetry.

Rather than focusing only on executing attacks, the project emphasizes understanding the complete attack-and-defense lifecycle — from generating malicious activity to identifying relevant telemetry, investigating events in Splunk, and applying appropriate mitigations.

## 📊 Security Monitoring & Telemetry

To provide visibility across the Active Directory environment, multiple Windows logging and monitoring mechanisms were configured.


## 🏗️ Lab Architecture

The lab consists of four virtual machines deployed using VMware Workstation:

| System | Role | Operating System |
|---|---|---|
| DC01 | Active Directory Domain Controller | Windows Server 2022 |
| WIN10 | Domain-Joined Endpoint | Windows 10 |
| KALI | Attacker Machine | Kali Linux |
| SPLUNK01 | SIEM Server | Ubuntu Desktop |

### Domain

`corp.local`

### Network

The systems communicate through an isolated VMware Host-only network, while separate NAT interfaces provide Internet connectivity when required.


### Telemetry Sources

- Windows Security Event Logs
- Sysmon
- PowerShell Operational Logs
- Advanced Windows Audit Policies
- Process Creation Logging
- Kerberos Authentication Events

Splunk Universal Forwarders were deployed on the Windows systems to forward security telemetry to the centralized Splunk Enterprise server.

This provided a single location for searching, correlating, and investigating activity occurring across the Active Directory environment.


## ⚔️ Attack Simulations

After establishing the Active Directory environment and telemetry pipeline, controlled attack simulations were performed from the Kali Linux attacker system.

The following techniques were tested:

### 1. Password Spraying

Authentication attempts were performed against multiple domain accounts to simulate password spraying behavior.

The resulting authentication failures were investigated in Splunk to identify patterns involving multiple accounts targeted within a short period.

### 2. AS-REP Roasting

An intentionally vulnerable account with Kerberos pre-authentication disabled was identified and used to demonstrate AS-REP Roasting.

The generated Kerberos authentication activity was investigated using Windows Security Event ID `4768`.

### 3. Credential Dumping

Credential material was extracted from the Domain Controller in the controlled lab to demonstrate the impact of privileged system compromise.

### 4. Pass-the-Hash

A recovered NTLM hash was reused to demonstrate authentication without requiring the account's plaintext password.

The resulting authentication activity was then investigated through the centralized Splunk telemetry.


## 🔎 Detection Engineering

The defensive portion of the project focuses on translating raw Windows and Active Directory telemetry into actionable detections.

Splunk was used to investigate authentication and endpoint activity generated during the attack simulations.

Detection scenarios include:

- Password spraying behavior
- Suspicious Kerberos authentication activity
- AS-REP Roasting indicators
- Unusual privileged authentication
- NTLM authentication activity
- Suspicious endpoint and process activity

The goal is to move beyond simple log collection and develop practical SOC-style detection and investigation workflows.


## 🛠️ Technologies Used

- Windows Server 2022
- Active Directory Domain Services
- Windows 10
- Kali Linux
- Ubuntu
- Splunk Enterprise
- Splunk Universal Forwarder
- Sysmon
- Windows Event Logging
- PowerShell Logging
- Group Policy
- VMware Workstation


## 📄 Project Documentation

A complete technical report documenting the design, deployment, configuration, attack simulations, security monitoring, detection process, troubleshooting, results, and mitigations was created as part of this project.

The full report will be available in this repository.


## ⚠️ Disclaimer

This project was created in a controlled and isolated home lab environment for educational and defensive security research purposes only.

All attack simulations were performed against systems owned and configured specifically for this lab. The techniques demonstrated in this repository should only be used in environments where explicit authorization has been granted.



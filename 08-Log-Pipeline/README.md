# Log Pipeline

This section documents the telemetry flow, log collection architecture, and detection pipeline used within the SOC Homelab Enterprise environment.

The objective is to simulate enterprise-style security visibility across endpoints, Active Directory, network traffic, IDS telemetry, firewall logs, and cloud-connected systems.

---

## Log Pipeline Objectives

The environment was designed to:

* Centralize security telemetry
* Simulate real-world SIEM ingestion
* Support detection engineering
* Enable incident investigations
* Correlate endpoint and network activity
* Monitor authentication events
* Validate attack simulations
* Provide cloud-connected visibility

---

## Telemetry Architecture

The lab collects telemetry from multiple layers of the environment.

```text
Windows Endpoints
        +
Active Directory
        ↓
Sysmon + Windows Events
        ↓
Splunk Enterprise
        +
Wazuh XDR

Network Traffic
        ↓
FortiGate
        +
Suricata IDS
        ↓
Splunk Enterprise
        +
Wazuh XDR

AWS-HUB
        ↓
Splunk Universal Forwarder
        +
Wazuh Agent
        ↓
Splunk Enterprise
        +
Wazuh XDR
```

---

## Primary Log Sources

| Source             | Type                             | Destination    |
| ------------------ | -------------------------------- | -------------- |
| Sysmon             | Endpoint telemetry               | Splunk + Wazuh |
| Windows Event Logs | Endpoint security logs           | Splunk + Wazuh |
| Active Directory   | Authentication and identity logs | Splunk + Wazuh |
| Suricata IDS       | Network telemetry                | Splunk + Wazuh |
| FortiGate          | Firewall and network logs        | Splunk + Wazuh |
| AWS-HUB            | Cloud telemetry                  | Splunk + Wazuh |

---

## Endpoint Telemetry

### Sysmon

Sysmon is deployed on all Windows systems to provide advanced endpoint visibility.

Monitored telemetry includes:

* Process creation
* Parent-child process relationships
* Network connections
* PowerShell activity
* Registry modifications
* Persistence mechanisms
* DNS queries
* LOLBins activity
* WMI activity
* Named pipe creation

### Windows Systems

| Host          | Role                               |
| ------------- | ---------------------------------- |
| WIN11-USER-01 | Domain-Joined Windows 11 Endpoint  |
| WIN11-USER-02 | Domain-Joined Windows 11 Endpoint  |
| DC01          | Active Directory Domain Controller |

Both Windows endpoints are joined to the SOCLAB.LOCAL Active Directory domain and generate endpoint telemetry used for monitoring, detection engineering, and investigation workflows.

---

## Active Directory Telemetry

### SOCLAB.LOCAL Domain

The Active Directory environment provides centralized authentication and identity telemetry.

Collected events include:

* User authentication activity
* Failed logon attempts
* Group membership changes
* Account management events
* Privilege escalation events
* Domain administration activity
* Group Policy activity

This telemetry provides visibility into identity-based attacks and authentication behavior commonly monitored within enterprise SOC environments.

---

## Suricata IDS Pipeline

Suricata operates as a dedicated passive IDS sensor using FortiSwitch SPAN monitoring.

Detection flow:

```text
Network Traffic
        ↓
FortiSwitch SPAN
        ↓
Physical Suricata Sensor
        ↓
EVE JSON
        ↓
Splunk Enterprise
        +
Wazuh XDR
        ↓
Alert / Dashboard / Investigation
```

Collected telemetry includes:

* HTTP requests
* DNS activity
* TLS metadata
* Network flows
* SQL Injection activity
* Brute Force attempts
* IDS alerts
* Reconnaissance activity
* Attack simulation telemetry

---

## Splunk Enterprise Pipeline

Splunk Enterprise functions as the primary SIEM platform.

Primary responsibilities:

* Centralized log ingestion
* Security dashboards
* Detection engineering
* Timeline reconstruction
* Alert correlation
* Threat visibility
* MITRE ATT&CK mapping

Primary log sources include:

* Sysmon
* Windows Event Logs
* Active Directory logs
* Suricata EVE JSON
* FortiGate logs
* AWS telemetry

---

## Wazuh XDR Pipeline

Wazuh functions as a secondary SIEM and XDR platform.

Primary responsibilities:

* Alerting
* Event correlation
* Endpoint monitoring
* Rule-based detections
* Security visibility
* Incident response support

Wazuh receives telemetry from:

* Sysmon
* Windows Event Logs
* Active Directory
* Suricata IDS
* Authentication logs
* AWS-HUB

---

## FortiGate Logging

FortiGate provides:

* Firewall traffic logs
* Inter-VLAN visibility
* VPN events
* Security policy logs
* Administrative activity
* Routing events

Forwarded telemetry:

```text
FortiGate
      ↓
Splunk Enterprise
      +
Wazuh XDR
```

This provides visibility into traffic flows across all network segments.

---

## AWS-HUB Telemetry

AWS-HUB extends monitoring capabilities beyond the local environment.

Components deployed:

* Splunk Universal Forwarder
* Wazuh Agent
* IPSec VPN Connectivity

Collected telemetry includes:

* Linux authentication events
* System logs
* Service activity
* VPN-related connectivity events
* Cloud infrastructure telemetry

AWS-HUB forwards logs into both Splunk Enterprise and Wazuh XDR through encrypted connectivity.

---

## Example Detection Flow

### SQL Injection Simulation

```text
KALI-01 (RED_TEAM)
        ↓
DVWA / Juice Shop
        ↓
Suricata Detection
        ↓
EVE JSON
        ↓
Splunk Enterprise
        +
Wazuh XDR
        ↓
Alert / Dashboard
        ↓
Incident Investigation
```

### Brute Force Simulation

```text
KALI-01 (RED_TEAM)
        ↓
DVWA Authentication Target
        ↓
Suricata Detection
        ↓
Splunk Enterprise
        +
Wazuh XDR
        ↓
Detection Rule Trigger
        ↓
Investigation Workflow
```

---

## Log Visibility Goals

The pipeline is designed to provide visibility into:

* Endpoint activity
* Authentication behavior
* Active Directory events
* Network attacks
* Web exploitation
* Threat simulations
* Administrative activity
* Firewall activity
* Cloud-connected infrastructure

---

## Current Pipeline Status

| Component                 | Status        |
| ------------------------- | ------------- |
| Sysmon → Splunk           | ✅ Operational |
| Sysmon → Wazuh            | ✅ Operational |
| Active Directory → Splunk | ✅ Operational |
| Active Directory → Wazuh  | ✅ Operational |
| Suricata → Splunk         | ✅ Operational |
| Suricata → Wazuh          | ✅ Operational |
| FortiGate → Splunk        | ✅ Operational |
| FortiGate → Wazuh         | ✅ Operational |
| AWS-HUB → Splunk          | ✅ Operational |
| AWS-HUB → Wazuh           | ✅ Operational |
| Detection Correlation     | ✅ Active      |

---

## Skills Demonstrated

* SIEM Engineering
* Detection Engineering
* Telemetry Correlation
* Log Pipeline Design
* Active Directory Monitoring
* IDS Monitoring
* Firewall Telemetry
* Endpoint Visibility
* Security Monitoring
* Threat Detection
* SOC Operations
* Windows Telemetry Analysis
* Cloud Security Visibility
* Splunk Administration
* Wazuh Administration

---

## Pipeline Summary

The SOC Homelab Enterprise log pipeline combines endpoint telemetry, Active Directory visibility, IDS monitoring, firewall telemetry, cloud infrastructure logs, and SIEM correlation to simulate enterprise SOC monitoring workflows.

The architecture enables realistic detection engineering, telemetry validation, attack visibility, incident investigation, and security monitoring across endpoint, network, authentication, firewall, and cloud-connected environments.

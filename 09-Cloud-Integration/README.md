# Cloud Integration

This section documents the cloud-connected architecture implemented within the SOC Homelab Enterprise environment.

The environment integrates AWS infrastructure with the on-premises SOC lab through a site-to-site IPSec VPN, providing secure connectivity, cloud telemetry collection, centralized monitoring, and enterprise-style hybrid infrastructure visibility.

---

## Cloud Integration Goals

The cloud environment was designed to:

* Simulate hybrid enterprise infrastructure
* Integrate cloud and on-premises security monitoring
* Support secure remote administration
* Centralize cloud telemetry collection
* Practice VPN architecture and troubleshooting
* Extend SOC visibility beyond the local network
* Support SIEM and XDR monitoring of cloud assets

---

## Cloud Architecture Overview

The cloud environment is connected to the SOC lab through a dedicated IPSec VPN tunnel between AWS and the FortiGate firewall.

```text
Remote MacBook Pro
        ↓
AWS-HUB
        ↓
IPSec VPN
        ↓
FortiGate 60F
        ↓
SOC Homelab Network

SOC_NET
SERVER_NET
USER_NET
MGMT_NET
DMZ_NET
RED_TEAM
```

This architecture provides secure communication between cloud infrastructure and on-premises systems without exposing internal services directly to the internet.

---

## AWS-HUB

### Purpose

AWS-HUB serves as a cloud-based infrastructure node integrated into the SOC environment.

Primary functions include:

* Cloud telemetry generation
* Secure VPN connectivity
* Hybrid infrastructure monitoring
* Remote administration support
* Splunk log forwarding
* Wazuh endpoint monitoring
* IPSec tunnel validation and troubleshooting

---

## AWS Platform

| Component        | Technology                               |
| ---------------- | ---------------------------------------- |
| Cloud Provider   | AWS                                      |
| Service          | EC2                                      |
| Operating System | Ubuntu Server 22.04                      |
| Role             | AWS-HUB                                  |
| Connectivity     | IPSec VPN                                |
| Monitoring       | Splunk Universal Forwarder + Wazuh Agent |

---

## Site-to-Site IPSec Connectivity

A dedicated IPSec VPN tunnel connects AWS-HUB and the FortiGate firewall.

```text
AWS-HUB
      ↕
IPSec VPN
      ↕
FortiGate 60F
```

Purpose:

* Secure communication
* Hybrid network connectivity
* Cloud-to-lab monitoring
* Encrypted traffic transport
* Enterprise VPN architecture

The tunnel provides secure access between AWS resources and internal SOC infrastructure.

---

## Remote Administration Architecture

The environment supports secure remote administration from external networks.

Primary administration device:

| Device               | Purpose                           |
| -------------------- | --------------------------------- |
| MacBook Pro (M1 Max) | Remote SOC Operations Workstation |

Remote administration workflow:

```text
MacBook Pro
      ↓
AWS-HUB
      ↓
IPSec VPN
      ↓
FortiGate
      ↓
SOC Environment
```

This design allows secure access to internal resources without exposing management interfaces directly to the public internet.

Administrative access includes:

* Splunk dashboards
* Wazuh monitoring
* FortiGate administration
* Active Directory management
* Incident investigations
* Detection engineering
* Infrastructure troubleshooting

---

## Cloud Telemetry Pipeline

AWS-HUB is monitored as a production-style Linux asset.

Telemetry sources include:

* Linux authentication logs
* System activity
* Service activity
* Network events
* VPN-related events
* Administrative activity

Telemetry flow:

```text
AWS-HUB
      ↓
Splunk Universal Forwarder
      ↓
Splunk Enterprise

AWS-HUB
      ↓
Wazuh Agent
      ↓
Wazuh Manager
```

This provides visibility into cloud-hosted infrastructure from both monitoring platforms.

---

## Security Monitoring Integration

AWS-HUB is fully integrated into the SOC monitoring stack.

### Splunk Enterprise

Used for:

* Log ingestion
* Cloud monitoring
* Search and investigation
* Dashboard visibility

### Wazuh XDR

Used for:

* Endpoint monitoring
* Alerting
* File integrity monitoring
* Linux security visibility

---

## Security Design Principles

The cloud architecture follows several security principles:

* Encrypted communications
* Network segmentation
* Centralized monitoring
* Controlled connectivity
* Least privilege access
* Hybrid infrastructure visibility
* No direct exposure of internal SOC services

---

## Skills Demonstrated

* AWS Fundamentals
* Hybrid Infrastructure Design
* IPSec VPN Deployment
* FortiGate VPN Configuration
* Linux Administration
* Splunk Administration
* Wazuh Administration
* Cloud Security Monitoring
* Telemetry Collection
* Log Forwarding
* Infrastructure Troubleshooting
* Secure Remote Access Design
* SOC Monitoring Operations

---

## Cloud Integration Summary

The SOC Homelab Enterprise cloud environment extends monitoring capabilities beyond the local network by integrating AWS infrastructure with on-premises SOC systems through an IPSec VPN connection.

AWS-HUB functions as a monitored cloud asset that forwards telemetry into both Splunk Enterprise and Wazuh XDR while also serving as a secure access layer for remote SOC administration from a dedicated MacBook Pro workstation.

This architecture simulates a realistic hybrid enterprise environment that combines cloud infrastructure, secure remote access, centralized monitoring, and enterprise security operations workflows.

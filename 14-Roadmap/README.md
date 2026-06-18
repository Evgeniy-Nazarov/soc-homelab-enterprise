# Roadmap

This section documents the evolution, completed milestones, current priorities, and future development plans for the SOC Homelab Enterprise environment.

The project was built incrementally to simulate a realistic enterprise Security Operations Center (SOC) with enterprise network segmentation, Active Directory, IDS monitoring, SIEM operations, detection engineering, incident investigations, and cloud-connected infrastructure.

---

## Completed Milestones

### Phase 1 — Core Infrastructure

Completed:

* Windows Server 2022 deployment
* Hyper-V virtualization platform
* Enterprise virtual networking
* Multi-VLAN architecture design
* Infrastructure deployment and validation

Status:

```text
Completed
```

---

### Phase 2 — Active Directory Deployment

Completed:

* Active Directory Domain Services (AD DS)
* DNS Services
* DHCP Services
* SOCLAB.LOCAL domain creation
* Organizational Unit structure
* Group Policy deployment
* Domain-joined Windows endpoints

Status:

```text
Completed
```

---

### Phase 3 — Enterprise Network Segmentation

Completed:

* VLAN 10 — SOC_NET
* VLAN 20 — USER_NET
* VLAN 30 — SERVER_NET
* VLAN 40 — MGMT_NET
* VLAN 50 — DMZ_NET
* VLAN 60 — HOME_NET
* VLAN 70 — GUEST_NET
* VLAN 80 — RED_TEAM

Status:

```text
Completed
```

---

### Phase 4 — Enterprise Network Modernization

Completed:

#### pfSense → FortiGate 60F

* Firewall migration
* Security policy redesign
* Inter-VLAN routing
* IPSec VPN deployment
* Enterprise firewall administration

#### TP-Link → FortiSwitch 124E

* VLAN trunking
* SPAN monitoring
* Enterprise switching
* Traffic visibility improvements

Status:

```text
Completed
```

---

### Phase 5 — SIEM & XDR Deployment

Completed:

#### Splunk Enterprise

* Primary SIEM deployment
* Log ingestion pipelines
* Security dashboards
* Search and investigation workflows

#### Wazuh XDR

* Endpoint monitoring
* Alerting and correlation
* Security visibility
* Agent management

Status:

```text
Completed
```

---

### Phase 6 — Network Security Monitoring

Completed:

#### Physical Suricata Sensor

* Dedicated IDS sensor
* SPAN monitoring
* EVE JSON telemetry
* Splunk integration
* Wazuh integration
* Enterprise network visibility

Status:

```text
Completed
```

---

### Phase 7 — Endpoint Visibility

Completed:

#### Sysmon Deployment

* Process creation monitoring
* PowerShell visibility
* Registry monitoring
* Network connection monitoring
* DNS visibility
* Endpoint telemetry collection

Status:

```text
Completed
```

---

### Phase 8 — Cloud Integration

Completed:

#### AWS-HUB

* AWS EC2 deployment
* IPSec VPN connectivity
* Splunk Universal Forwarder
* Wazuh Agent
* Hybrid monitoring architecture
* Secure remote administration platform

Status:

```text
Completed
```

---

### Phase 9 — Attack Simulation Environment

Completed:

#### Attack Platforms

* Kali Linux (RED_TEAM VLAN)
* DVWA
* OWASP Juice Shop

#### Detection Engineering

* SQL Injection Detection
* Hydra Brute Force Detection
* Custom Wazuh Rules
* Custom Splunk Detections
* MITRE ATT&CK Mapping

Status:

```text
Completed
```

---

## Current Focus

### Portfolio Development

Current priorities:

* GitHub documentation
* Architecture documentation
* Detection engineering documentation
* Dashboard documentation
* Incident investigation write-ups
* Attack simulation reporting
* Screenshot standardization

Status:

```text
In Progress
```

---

### Incident Response Portfolio

Current work:

* Cydeo SOC investigations
* Timeline reconstruction
* IOC analysis
* Root cause analysis
* MITRE ATT&CK mapping
* Professional case documentation

Status:

```text
In Progress
```

---

## Next Phase

### Professional Portfolio Completion

Planned:

* Complete GitHub repository
* Update architecture diagrams
* Complete attack simulation documentation
* Finalize incident investigations
* Complete screenshot library

Priority:

```text
High
```

---

### Career Preparation

Planned:

* LinkedIn optimization
* Resume refinement
* Interview preparation
* SOC analyst interview labs
* Threat analysis practice

Priority:

```text
High
```

---

## Planned Monitoring Enhancements

### Zeek Integration

Planned:

* Deploy Zeek on the physical Suricata sensor
* Network metadata collection
* Enhanced DNS visibility
* HTTP protocol analysis
* Threat hunting support

Purpose:

Provide deeper network visibility and investigation capabilities beyond IDS alerts.

---

### Vulnerability Management

Planned:

* Nessus Essentials deployment
* Internal vulnerability assessments
* Security baseline validation
* Vulnerability reporting workflows

Purpose:

Introduce vulnerability management and security assessment capabilities.

---

### Network Forensics

Planned:

* Wireshark deployment on Mac Studio
* Packet capture analysis
* Protocol troubleshooting
* Traffic validation

Purpose:

Provide packet-level visibility for investigations and network analysis.

---

### Endpoint Expansion

Planned:

* Additional Windows 11 workstation
* Expanded Active Directory environment
* Lateral movement simulation scenarios
* Multi-endpoint detection testing

Purpose:

Improve enterprise realism and attack simulation capabilities.

---

## Long-Term Goal

Build a realistic enterprise-style SOC environment capable of demonstrating:

* Security Monitoring
* Detection Engineering
* Incident Response
* SIEM Operations
* Active Directory Administration
* IDS Monitoring
* Cloud Security Monitoring
* Threat Hunting
* Vulnerability Management
* Hybrid Infrastructure Monitoring

The project is designed to support continuous learning, portfolio development, and preparation for enterprise SOC Analyst and Cybersecurity Operations roles.

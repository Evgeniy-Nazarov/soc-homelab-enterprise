# SOC Lab Evolution Archive

## Overview

This document chronicles the evolution of the SOC Homelab Enterprise environment from a learning-focused cybersecurity lab into a realistic enterprise-style Security Operations Center (SOC) platform.

The project evolved through multiple infrastructure redesigns, platform migrations, monitoring improvements, troubleshooting efforts, and architectural decisions aimed at increasing operational maturity, security visibility, and enterprise relevance.

The purpose of this archive is to document the engineering journey behind the environment and highlight the lessons learned throughout its development.

---

# Phase 1 — Initial Lab Foundation

The original environment was created to provide hands-on experience with security monitoring, virtualization, Active Directory, and attack simulation.

### Initial Objectives

* Learn SOC workflows
* Gain practical cybersecurity experience
* Build security visibility
* Deploy monitoring platforms
* Create an attack simulation environment
* Improve incident investigation skills

### Initial Infrastructure

* Hyper-V Virtualization
* Windows Server
* Active Directory
* Basic VLAN Segmentation
* pfSense Firewall
* TP-Link Managed Switch
* Virtual Suricata IDS
* Wazuh
* QRadar Community Edition

### Outcome

The initial environment successfully provided a foundation for learning security operations and infrastructure administration.

---

# Phase 2 — Enterprise Firewall Migration

As the environment expanded, limitations of the original firewall platform became more apparent.

### Original Platform

```text
pfSense
```

### Challenges

* Operational instability during extended uptime
* Increased administrative complexity
* Limited exposure to enterprise firewall workflows
* Reduced alignment with enterprise environments

### Engineering Decision

```text
pfSense
      ↓
FortiGate 60F
```

### Results

* Improved stability
* Enterprise firewall administration experience
* Better VLAN management
* Improved security policy visibility
* More realistic SOC architecture

---

# Phase 3 — Enterprise Switching Migration

To improve segmentation and monitoring capabilities, the switching infrastructure was upgraded.

### Original Platform

```text
TP-Link Managed Switch
```

### Engineering Decision

```text
TP-Link
      ↓
FortiSwitch 124E
```

### Reasons

* Enterprise switching experience
* Improved VLAN management
* Better FortiGate integration
* Reliable SPAN monitoring
* Enhanced visibility

### Results

* Improved segmentation
* Better operational consistency
* Enterprise switching workflows
* Enhanced monitoring architecture

---

# Phase 4 — IDS Monitoring Evolution

One of the most significant improvements involved the network monitoring architecture.

### Original Design

```text
Virtual Suricata IDS
```

Traffic visibility relied primarily on Hyper-V virtual switching and mirrored traffic.

### Challenges

* Limited packet visibility
* Reduced monitoring reliability
* Inconsistent cross-VLAN visibility
* Limited forensic capability

### Engineering Decision

```text
Virtual Suricata
          ↓
Physical Suricata Sensor
```

### Final Architecture

```text
FortiSwitch SPAN Port
            ↓
Physical Suricata IDS
            ↓
Splunk Enterprise
            ↓
Wazuh XDR
```

### Results

* Full packet visibility
* Reliable IDS monitoring
* Improved attack telemetry
* Better forensic visibility
* Enterprise-style network security monitoring

---

# Phase 5 — SIEM Evolution

The monitoring stack evolved significantly throughout development.

### Initial Evaluation

```text
QRadar Community Edition
```

### Challenges

* High resource consumption
* Increased operational complexity
* Limited practicality for a home lab environment

### Engineering Decision

```text
QRadar
     ↓
Splunk Enterprise + Wazuh XDR
```

### Results

* Greater flexibility
* Better dashboard customization
* Improved troubleshooting workflows
* Stronger detection engineering capabilities
* Increased industry relevance

---

# Phase 6 — Detection Engineering Growth

The environment gradually evolved from basic log collection into a detection engineering platform.

### Early Focus

* Log ingestion validation
* Agent deployment
* Telemetry verification
* Basic monitoring

### Expanded Capabilities

* SQL Injection detection
* Alert validation
* Detection tuning
* MITRE ATT&CK mapping
* Telemetry analysis
* Cross-platform correlation
* Investigation workflows

### Results

* Improved detection quality
* Better alert fidelity
* Practical SOC experience
* Investigation readiness

---

# Phase 7 — Cloud Connectivity Evolution

Cloud integration was introduced to support hybrid monitoring and remote administration.

### Initial Connectivity

```text
WireGuard
```

WireGuard was originally used for cloud connectivity and remote administration.

### Evolution

As the environment matured, FortiGate-based site-to-site VPN connectivity became the preferred solution.

### Current Architecture

```text
AWS EC2
        ↓
Site-to-Site IPsec VPN
        ↓
FortiGate 60F
        ↓
SOC Environment
```

### Results

* Secure cloud connectivity
* Centralized monitoring
* Hybrid SOC architecture
* Cross-environment visibility

---

# Phase 8 — Network Segmentation Expansion

The original network design evolved into a fully segmented enterprise-style architecture.

### Initial Segmentation

* User Network
* Server Network
* Monitoring Network

### Current Security Zones

| Zone       | Purpose                                      |
| ---------- | -------------------------------------------- |
| SOC_NET    | Security Monitoring Infrastructure           |
| USER_NET   | Corporate Endpoints                          |
| SERVER_NET | Active Directory and Infrastructure Services |
| MGMT_NET   | Administrative Management Network            |
| DMZ_NET    | Vulnerable Applications                      |
| HOME_NET   | Trusted Personal Devices                     |
| GUEST_WIFI | Internet-Only Wireless Access                |
| RED_TEAM   | Attack Simulation Environment                |

### Results

* Reduced attack surface
* Better access control
* Improved monitoring visibility
* More realistic enterprise architecture

---

# Phase 9 — Enterprise Security Architecture

The environment ultimately evolved into a fully integrated security operations platform.

### Security Infrastructure

* FortiGate 60F
* FortiSwitch 124E
* Physical Suricata IDS Sensor
* Splunk Enterprise
* Wazuh XDR

### Identity Infrastructure

* Windows Server 2022
* Active Directory
* DNS
* DHCP
* Group Policy
* Sysmon

### Attack Simulation Infrastructure

* Kali Linux
* OWASP Juice Shop
* DVWA

### Cloud Infrastructure

* AWS EC2
* Site-to-Site IPsec VPN

### Monitoring Architecture

```text
Endpoints
Servers
Active Directory
AWS
FortiGate
Suricata
        ↓
Splunk Enterprise
        +
Wazuh XDR
```

---

# Major Engineering Lessons Learned

Key lessons learned throughout development include:

* Stability is more valuable than unnecessary complexity.
* Enterprise technologies provide more realistic operational experience.
* Physical IDS monitoring significantly improves network visibility.
* Effective segmentation reduces risk and improves monitoring quality.
* Detection engineering requires continuous validation and tuning.
* Documentation improves consistency and troubleshooting efficiency.
* Security monitoring platforms are only as effective as the telemetry they receive.
* Continuous improvement is a core component of security operations.

---

# Final Outcome

The environment evolved from a learning-focused cybersecurity lab into a realistic enterprise-style SOC platform capable of supporting:

* SIEM Engineering
* Detection Engineering
* Network Security Monitoring
* Incident Investigation
* Threat Monitoring
* Active Directory Security
* Firewall Engineering
* Cloud Security Integration
* Security Operations Workflows
* SOC Analyst Skill Development

The project continues to evolve through new detections, investigations, attack simulations, monitoring enhancements, and enterprise security engineering improvements.

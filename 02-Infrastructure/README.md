# Infrastructure

This section documents the physical and virtual infrastructure supporting the SOC Homelab Enterprise environment.

The lab combines enterprise-style network segmentation, virtualization, SIEM platforms, endpoint telemetry, Active Directory services, IDS monitoring, cloud integration, and attack simulation capabilities.

The objective was to design and manually build a realistic enterprise-style Security Operations Center (SOC) environment focused on blue-team operations, detection engineering, security monitoring, incident investigation, and SIEM administration.

## Infrastructure Goals

The environment was designed to support:

* Enterprise-style SOC workflows
* SIEM engineering
* Detection engineering
* IDS monitoring
* Attack simulation
* Active Directory visibility
* Endpoint telemetry
* Cloud-connected security monitoring
* Enterprise network segmentation
* Long-term scalability

Additional planning included maintaining a mixed-use environment capable of supporting both cybersecurity workloads and everyday home use.

---

## Hardware Selection & Planning

The infrastructure was designed around:

* Virtualization performance
* Multi-VM scalability
* Large memory capacity
* SIEM workload support
* Detection engineering
* Enterprise-style segmentation
* Stability and reliability
* Long-term infrastructure growth

The environment was manually planned and assembled to support realistic SOC workflows and enterprise security monitoring.

---

# Physical Hardware

## HomeLab Server (Primary Hypervisor)

The core SOC environment runs on a dedicated virtualization platform.

| Component         | Specification                 |
| ----------------- | ----------------------------- |
| CPU               | Intel Core i9-14900K          |
| RAM               | 192 GB DDR5                   |
| Motherboard       | ASUS ROG Maximus Z790 Hero    |
| Primary Storage   | 4 TB NVMe SSD                 |
| Secondary Storage | 1 TB Samsung SATA SSD         |
| OS                | Windows Server 2022 + Hyper-V |
| Role              | Primary Virtualization Host   |

### Purpose

* Hosts core virtual machines
* SIEM infrastructure
* Active Directory services
* Security monitoring systems
* Attack simulation environment
* Detection engineering workflows

---

## Mac Studio (Primary SOC Administration Workstation)

Primary workstation used for SOC administration and monitoring.

| Component        | Specification                   |
| ---------------- | ------------------------------- |
| Model            | Mac Studio                      |
| CPU              | Apple M2 Ultra                  |
| RAM              | 64 GB                           |
| Storage          | 1 TB SSD                        |
| External Storage | OWC Thunderbolt 5 4 TB SSD      |
| Role             | SOC Administration & Monitoring |

### Primary Uses

* FortiGate administration
* Splunk monitoring
* Wazuh monitoring
* Dashboard engineering
* Detection engineering
* Documentation
* GitHub portfolio development

---

## MacBook Pro (Remote Administration Platform)

Dedicated remote access workstation.

| Component | Specification            |
| --------- | ------------------------ |
| Model     | MacBook Pro 16"          |
| CPU       | Apple M1 Max             |
| RAM       | 32 GB                    |
| Storage   | 1 TB SSD                 |
| Role      | Secure Remote SOC Access |

### Primary Uses

* Remote administration
* VPN connectivity
* AWS HUB access
* External monitoring
* SOC management

---

# Manual Hardware Assembly

The SOC HomeLab server was manually assembled to support enterprise-style cybersecurity operations.

Build process included:

* Hardware component selection
* Manual server assembly
* Storage planning
* Hypervisor deployment
* Memory sizing for multi-VM workloads
* Virtual network planning
* VLAN integration
* Resource optimization

This process improved practical infrastructure planning and troubleshooting experience.

---

# Why Hyper-V

Hyper-V was selected to support:

* Enterprise Windows integration
* Windows Server compatibility
* Stable virtualization
* VLAN-aware networking
* Enterprise-style administration
* Multi-VM resource management

---

# Network Interface Selection

## Intel I350-T4

A dedicated multi-port enterprise network adapter was selected to support segmented networking.

### Reasons for Selection

* Enterprise reliability
* Hyper-V compatibility
* VLAN trunking support
* Stable driver support
* Dedicated lab networking
* Multi-network segmentation

---

# Virtual Infrastructure

## SOC Infrastructure Systems

| Hostname  | IP Address    | Role                   |
| --------- | ------------- | ---------------------- |
| WAZUH-01  | 192.168.10.10 | Wazuh XDR Platform     |
| SPLUNK-01 | 192.168.10.20 | Splunk Enterprise SIEM |

---

## User Infrastructure

| Hostname      | IP Address    | Role                       |
| ------------- | ------------- | -------------------------- |
| WIN11-USER-01 | 192.168.20.10 | Windows Endpoint Telemetry |
| WIN11-USER-02 | 192.168.20.20 | Windows Endpoint Telemetry |

---

## Red Team Infrastructure

| Hostname | IP Address    | Role                       |
| -------- | ------------- | -------------------------- |
| KALI-01  | 192.168.80.10 | Attack Simulation Platform |

The dedicated RED_TEAM network provides isolated attack simulation capabilities used to validate detections, alerts, and SOC monitoring workflows.

---

## Server Infrastructure

| Hostname | IP Address    | Role                             |
| -------- | ------------- | -------------------------------- |
| DC01     | 192.168.30.10 | Active Directory, DNS, DHCP      |
| DB01     | 192.168.30.20 | Backend Database Server for DVWA |

The DVWA environment is intentionally segmented across multiple security zones.

The web application is hosted within the DMZ while the supporting database is located inside the SERVER_NET segment. Communication is controlled through FortiGate security policies to simulate enterprise application architecture.

---

## DMZ Infrastructure

| Hostname   | IP Address    | Role                         |
| ---------- | ------------- | ---------------------------- |
| DVWA       | 192.168.50.10 | Vulnerable Web Application   |
| Juice Shop | 192.168.50.20 | OWASP Vulnerable Application |

---

## Cloud Infrastructure

| Hostname | Platform       | Role                                                   |
| -------- | -------------- | ------------------------------------------------------ |
| AWS-HUB  | AWS EC2 Ubuntu | Cloud Integration, Log Collection, Secure Connectivity |

AWS-HUB is connected through IPSec VPN and forwards telemetry into both Splunk Enterprise and Wazuh XDR.

---

# Security Monitoring Infrastructure

| System                   | Role                                        |
| ------------------------ | ------------------------------------------- |
| Physical Suricata Sensor | Passive SPAN Monitoring                     |
| FortiGate 60F            | Firewall, Routing, Segmentation, VPN        |
| FortiSwitch 124E         | VLAN Switching, Trunking, SPAN              |
| Splunk Enterprise        | Primary SIEM                                |
| Wazuh XDR                | Detection, Correlation, Endpoint Monitoring |

---

# Hyper-V Virtualization Model

The SOC environment is hosted on Windows Server 2022 using Hyper-V virtualization.

Key design goals include:

* Enterprise segmentation
* Resource isolation
* Multi-SIEM visibility
* Attack simulation
* Security telemetry collection
* Secure administration
* Detection engineering
* SOC workflow simulation

---

# Infrastructure Philosophy

The environment was built around several core principles:

* Stability over complexity
* Enterprise realism
* Segmentation first
* Visibility over noise
* Practical learning
* Detection-driven monitoring
* Continuous improvement

---

# Skills Demonstrated

* Infrastructure Planning
* Hyper-V Virtualization
* Enterprise Networking
* VLAN Segmentation
* FortiGate Administration
* FortiSwitch Administration
* SIEM Engineering
* IDS Monitoring
* Active Directory Administration
* Endpoint Telemetry
* Detection Engineering
* Security Monitoring
* AWS Integration
* Cloud Connectivity
* Enterprise SOC Architecture

---

# Infrastructure Summary

The SOC Homelab Enterprise infrastructure was manually designed and assembled to simulate a realistic enterprise Security Operations Center (SOC) environment.

The architecture combines enterprise networking, virtualization, Active Directory, IDS monitoring, endpoint telemetry, SIEM engineering, attack simulation, cloud integration, and secure remote administration to support practical SOC analyst development and enterprise security engineering experience.

The environment continues to evolve through new detections, dashboards, incident investigations, attack simulations, and monitoring improvements while maintaining enterprise design principles and operational stability.

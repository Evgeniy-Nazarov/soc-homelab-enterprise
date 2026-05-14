# Infrastructure

This section documents the physical and virtual infrastructure supporting the SOC Homelab Enterprise environment.

The lab combines enterprise-style networking, virtualization, SIEM platforms, endpoint telemetry, Active Directory services, IDS monitoring, and secure cloud-connected remote access.

The objective was to design and manually build a realistic enterprise-style Security Operations Center (SOC) environment focused on practical blue-team operations, SIEM engineering, detection engineering, and incident monitoring.

---

## Infrastructure Goals

The environment was designed to support:

- Enterprise-style SOC workflows
- SIEM engineering
- Detection engineering
- IDS monitoring
- Attack simulation
- Active Directory visibility
- Endpoint telemetry
- Secure cloud-connected remote access
- Enterprise network segmentation
- Long-term scalability

Additional planning included maintaining a mixed-use environment capable of supporting both cybersecurity workloads and everyday home use.

---

## Hardware Selection & Planning

The infrastructure was designed around:

- Virtualization performance
- Multi-VM scalability
- Large memory capacity
- SIEM workload support
- Detection engineering
- Enterprise-style segmentation
- Stability and reliability
- Long-term infrastructure growth

The environment was manually planned and assembled to support realistic SOC workflows and enterprise-style security monitoring.

---

## Physical Hardware

### HomeLab Server (Primary Hypervisor)

The core SOC environment runs on a manually built virtualization platform.

| Component | Specification |
|-----------|----------------|
| CPU | Intel Core i9-14900K |
| RAM | 128 GB DDR5 |
| Primary Storage | 4 TB NVMe SSD |
| Secondary Storage | 1 TB Samsung SATA SSD |
| Role | Hyper-V virtualization host |
| OS | Windows Server 2022 + Hyper-V |

Purpose:

- Hosts core virtual machines
- SIEM infrastructure
- Active Directory
- Attack simulation environment
- Security telemetry collection
- Detection engineering workflows

---

### Mac Studio (Primary SOC Administration Workstation)

Primary workstation used for SOC administration and monitoring.

| Component | Specification |
|-----------|----------------|
| Model | Mac Studio |
| CPU | Apple M2 Ultra |
| RAM | 64 GB |
| Storage | 1 TB SSD |
| External Storage | OWC 4 TB SSD (Thunderbolt) |
| Role | SOC administration & monitoring |

Primary uses:

- FortiGate administration
- Splunk monitoring
- Wazuh monitoring
- Dashboard engineering
- Detection engineering
- Documentation
- GitHub portfolio development

---

### MacBook Pro (Remote Administration Platform)

Dedicated remote access workstation.

| Component | Specification |
|-----------|----------------|
| Model | MacBook Pro |
| CPU | Apple M1 Max |
| RAM | 32 GB |
| Storage | 1 TB SSD |
| Role | Secure remote SOC access |

Primary uses:

- Secure remote administration
- WireGuard VPN access
- AWS HUB connectivity
- External monitoring
- Remote SOC management

---

## Manual Hardware Assembly

The SOC HomeLab server was manually assembled to support enterprise-style cybersecurity operations.

Build process included:

- Hardware component selection
- Manual server assembly
- Storage planning
- Hypervisor deployment
- Memory sizing for multi-VM workloads
- Virtual network planning
- VLAN integration
- Resource optimization

This process improved practical infrastructure planning and troubleshooting experience.

---

## Why Hyper-V

Hyper-V was selected to support:

- Enterprise Windows integration
- Windows Server compatibility
- Stable virtualization
- VLAN-aware networking
- Enterprise-style administration
- Multi-VM resource management

---

## Network Interface Selection

### Intel I350-T4

A dedicated multi-port enterprise network adapter was selected to support segmented networking.

Reasons for selection:

- Enterprise reliability
- Hyper-V compatibility
- VLAN trunking support
- Stable driver support
- Dedicated lab networking
- Multi-network segmentation

---

## Virtual Infrastructure

### SOC Infrastructure Systems

| Hostname | IP Address | Role |
|----------|------------|------|
| WAZUH-01 | 192.168.10.10 | Wazuh XDR / Secondary SIEM |
| SPLUNK-01 | 192.168.10.20 | Splunk Enterprise / Primary SIEM |

---

### User & Attack Simulation Systems

| Hostname | IP Address | Role |
|----------|------------|------|
| WIN11-USER-01 | 192.168.20.10 | Windows workstation telemetry |
| KALI-01 | 192.168.20.20 | Attack simulation platform |

---

### Server Infrastructure

| Hostname | IP Address | Role |
|----------|------------|------|
| DC01 | 192.168.30.10 | Active Directory / DNS |
| DB01 | 192.168.30.20 | Database Server |

---

### DMZ Infrastructure

| Hostname | IP Address | Role |
|----------|------------|------|
| DVWA / WEB01 | 192.168.50.10 | Vulnerable web application |
| Juice Shop | 192.168.50.20:3000 | OWASP vulnerable application |

---

### Security Monitoring Infrastructure

| System | Role |
|--------|------|
| Suricata IDS (Physical Sensor) | Passive SPAN monitoring |
| FortiGate 60F | Firewall, routing, VPN |
| FortiSwitch 124E | VLAN switching and SPAN |

---

## Hyper-V Virtualization Model

The SOC environment is hosted on Windows Server 2022 using Hyper-V virtualization.

Key design goals include:

- Enterprise segmentation
- Resource isolation
- Multi-SIEM visibility
- Attack simulation
- Security telemetry
- Secure administration
- Detection engineering
- SOC workflow simulation

---

## Infrastructure Philosophy

The environment was built around several core principles:

- Stability over complexity
- Enterprise realism
- Segmentation first
- Visibility over noise
- Practical learning
- Detection-driven monitoring
- Continuous improvement

---

## Skills Demonstrated

- Infrastructure Planning
- Hyper-V Virtualization
- Enterprise Networking
- VLAN Segmentation
- SIEM Engineering
- IDS Monitoring
- Active Directory Administration
- Endpoint Telemetry
- Detection Engineering
- Security Monitoring
- Cloud-Connected Administration
- Enterprise SOC Architecture

---

## Infrastructure Summary

The SOC Homelab Enterprise infrastructure was manually designed and assembled to simulate a realistic enterprise Security Operations Center (SOC) environment.

The architecture combines physical networking, virtualization, Active Directory, IDS monitoring, endpoint telemetry, SIEM engineering, attack simulation, and secure cloud-connected administration to support practical SOC analyst development and enterprise security engineering experience.

This infrastructure continues to evolve as new detections, attack simulations, dashboards, and monitoring capabilities are added throughout the lab lifecycle.

# Infrastructure

This section documents the physical and virtual infrastructure supporting the SOC Homelab Enterprise environment.

The lab combines enterprise-style networking, virtualization, SIEM platforms, endpoint telemetry, Active Directory services, IDS monitoring, and secure cloud-connected remote access.

---

## Infrastructure Goals

- Simulate a real-world enterprise SOC environment
- Build hands-on SIEM engineering experience
- Practice blue-team monitoring and incident response
- Support attack simulation and detection engineering
- Maintain segmented infrastructure with centralized visibility
- Provide secure remote administration through cloud connectivity

---

## Physical Hardware

### HomeLab Server (Primary Hypervisor)

| Component | Specification |
|-----------|----------------|
| CPU | Intel Core i9-14900K |
| RAM | 128 GB DDR5 |
| Storage | 4 TB NVMe SSD + 1 TB Samsung SSD |
| Role | Hyper-V virtualization host |
| OS | Windows Server 2022 + Hyper-V |

Purpose:

- Hosts core virtual machines
- Supports SOC infrastructure
- Attack simulation environment
- Security telemetry collection
- SIEM platforms

---

### Mac Studio (Primary Admin Workstation)

| Component | Specification |
|-----------|----------------|
| Model | Mac Studio |
| CPU | Apple M2 Ultra |
| RAM | 64 GB |
| Storage | 1 TB SSD |
| External Storage | OWC 4 TB SSD (Thunderbolt 5) |
| Role | SOC administration & lab management |

Purpose:

- FortiGate administration
- SIEM monitoring
- Dashboard development
- Detection engineering
- Infrastructure management
- Documentation and GitHub portfolio

---

### MacBook Pro (Remote Administration)

| Component | Specification |
|-----------|----------------|
| Model | MacBook Pro |
| CPU | Apple M1 Max |
| RAM | 32 GB |
| Storage | 1 TB SSD |
| Role | Secure remote SOC access |

Purpose:

- Remote administration
- WireGuard VPN access
- AWS HUB connectivity
- External monitoring and management

---

## Virtual Infrastructure

### SOC Infrastructure Systems

| Hostname | IP Address | Role |
|----------|------------|------|
| WAZUH-01 | 192.168.10.10 | Wazuh XDR / SIEM |
| SPLUNK-01 | 192.168.10.20 | Splunk Enterprise SIEM |

---

### User & Attack Simulation Systems

| Hostname | IP Address | Role |
|----------|------------|------|
| WIN11-USER-01 | 192.168.20.10 | Windows workstation |
| KALI-01 | 192.168.20.20 | Attack simulation |

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
| Suricata IDS (Physical) | Passive SPAN monitoring |
| FortiGate 60F | Routing, firewall, VPN |
| FortiSwitch 124E | VLAN switching and SPAN |

---

## Hyper-V Virtualization Model

The SOC Homelab Enterprise environment is hosted on Windows Server 2022 using Hyper-V virtualization.

Key design goals include:

- Segmented enterprise architecture
- Resource isolation
- Attack simulation environment
- SIEM visibility
- Secure administrative access
- Enterprise-style monitoring workflows

---

## Infrastructure Summary

The environment combines:

- Physical enterprise networking
- Hyper-V virtualization
- Active Directory services
- Endpoint telemetry
- IDS monitoring
- Multi-SIEM visibility
- Cloud-connected remote access
- Detection engineering workflows
- Attack simulation capabilities

This infrastructure is continuously expanded to improve practical SOC analyst skills and enterprise security engineering experience.

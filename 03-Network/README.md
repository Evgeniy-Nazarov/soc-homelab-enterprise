# Network Architecture

This section documents the network segmentation, VLAN design, firewall architecture, switching model, IDS visibility, cloud connectivity, and traffic monitoring implemented within the SOC Homelab Enterprise environment.

The objective was to simulate a realistic enterprise-style security architecture with centralized visibility, secure routing, attack simulation capabilities, and enterprise monitoring workflows.

---

## Network Design Goals

The environment was designed to support:

* Enterprise network segmentation
* Secure inter-VLAN routing
* DMZ isolation
* IDS visibility
* Traffic monitoring
* Attack simulation
* Secure management access
* Cloud integration
* Zero Trust principles
* Enterprise SOC workflows

---

## VLAN Architecture

The network is segmented into multiple security zones.

| VLAN    | Network    | Subnet          | Purpose                               |
| ------- | ---------- | --------------- | ------------------------------------- |
| VLAN 10 | SOC_NET    | 192.168.10.0/24 | SIEM and security infrastructure      |
| VLAN 20 | USER_NET   | 192.168.20.0/24 | Domain-joined user workstations       |
| VLAN 30 | SERVER_NET | 192.168.30.0/24 | Active Directory and backend services |
| VLAN 40 | MGMT_NET   | 192.168.40.0/24 | Administrative management             |
| VLAN 50 | DMZ_NET    | 192.168.50.0/24 | Public-facing applications            |
| VLAN 60 | HOME_NET   | 192.168.60.0/24 | Home and media devices                |
| VLAN 70 | GUEST_NET  | 192.168.70.0/24 | Isolated guest Wi-Fi                  |
| VLAN 80 | RED_TEAM   | 192.168.80.0/24 | Attack simulation environment         |

---

## Core Network Components

### FortiGate 60F

Primary enterprise firewall responsible for:

* Inter-VLAN routing
* Security policy enforcement
* VPN connectivity
* IPSec cloud integration
* Traffic inspection
* Network segmentation
* Administrative access

Primary management interface:

```text
192.168.40.1
```

---

### FortiSwitch 124E

Managed switch responsible for:

* VLAN switching
* Port segmentation
* SPAN mirroring
* IDS visibility
* Trunking
* Traffic aggregation

---

## SPAN / Port Mirroring Architecture

Traffic visibility is achieved using a dedicated SPAN configuration.

```text
FortiGate
     +
Hyper-V Host
     ↓
FortiSwitch SPAN
     ↓
Physical Suricata Sensor
     ↓
Splunk Enterprise
     +
Wazuh XDR
```

This configuration provides:

* East-west visibility
* North-south visibility
* Inter-VLAN monitoring
* DMZ traffic monitoring
* User endpoint visibility
* Attack telemetry
* Security event collection

---

## Security Zones

### SOC_NET (VLAN 10)

Purpose:

* SIEM infrastructure
* Security monitoring
* Detection engineering

Systems:

| Host      | IP Address    |
| --------- | ------------- |
| WAZUH-01  | 192.168.10.10 |
| SPLUNK-01 | 192.168.10.20 |

---

### USER_NET (VLAN 20)

Purpose:

* Domain-joined user workstations
* Endpoint monitoring
* Authentication telemetry

Systems:

| Host          | IP Address    |
| ------------- | ------------- |
| WIN11-USER-01 | 192.168.20.10 |
| WIN11-USER-02 | 192.168.20.20 |

Both systems are joined to the SOCLAB.LOCAL Active Directory domain and generate Windows security and Sysmon telemetry.

---

### SERVER_NET (VLAN 30)

Purpose:

* Identity services
* Infrastructure services
* Backend application services

Systems:

| Host | IP Address    |
| ---- | ------------- |
| DC01 | 192.168.30.10 |
| DB01 | 192.168.30.20 |

DC01 serves as the primary Domain Controller for the SOCLAB.LOCAL environment and provides:

* Active Directory Domain Services
* DNS Services
* DHCP Services
* Group Policy Management
* Centralized Authentication

The backend database supporting DVWA resides within SERVER_NET and is separated from the application layer through network segmentation and firewall controls.

---

### MGMT_NET (VLAN 40)

Purpose:

* Administrative access
* Infrastructure management

Systems:

| Host                        | IP Address      |
| --------------------------- | --------------- |
| FortiGate Management        | 192.168.40.1    |
| Administrative Workstations | 192.168.40.0/24 |

---

### DMZ_NET (VLAN 50)

Purpose:

* Public-facing services
* Web application testing
* Attack simulation targets

Systems:

| Host       | IP Address    |
| ---------- | ------------- |
| DVWA       | 192.168.50.10 |
| Juice Shop | 192.168.50.20 |

The DVWA web application resides within the DMZ while its supporting database resides within SERVER_NET, simulating a common enterprise multi-tier application architecture.

---

### HOME_NET (VLAN 60)

Purpose:

* Personal devices
* Media services
* Daily household use

This network remains separated from SOC infrastructure and attack simulation environments.

---

### GUEST_NET (VLAN 70)

Purpose:

* Guest wireless access
* Internet-only connectivity

This network is isolated from all internal resources.

---

### RED_TEAM (VLAN 80)

Purpose:

* Adversary simulation
* Detection validation
* Security testing

Systems:

| Host    | IP Address    |
| ------- | ------------- |
| KALI-01 | 192.168.80.10 |

The RED_TEAM network provides a dedicated environment for offensive security testing while remaining isolated from production monitoring systems.

---

## Cloud Connectivity

### AWS-HUB

AWS-HUB provides secure cloud connectivity through an IPSec VPN tunnel integrated with the FortiGate firewall.

Functions include:

* Secure remote connectivity
* Log forwarding
* Splunk Universal Forwarder
* Wazuh Agent telemetry
* Hybrid monitoring architecture

Systems:

| Host    | Role                                     |
| ------- | ---------------------------------------- |
| AWS-HUB | Cloud Monitoring and Log Collection Node |

AWS-HUB forwards telemetry to both Splunk Enterprise and Wazuh XDR through encrypted connectivity.

---

## IDS Visibility

### Physical Suricata Sensor

Suricata operates as a dedicated passive IDS sensor connected to a SPAN destination port.

Capabilities include:

* HTTP monitoring
* DNS visibility
* TLS metadata
* SQL Injection detection
* Brute Force detection
* Attack visibility
* Security telemetry collection

Traffic visibility includes:

* VLAN-tagged traffic
* Inter-VLAN routing
* User workstation activity
* Active Directory traffic
* DMZ activity
* Attack simulation traffic
* Cloud-connected telemetry

---

## Zero Trust Design Principles

The network follows several security principles:

* Segmentation first
* Least privilege
* Controlled access
* Visibility-driven monitoring
* Isolated management
* Dedicated attack infrastructure
* Secure cloud connectivity

---

## Skills Demonstrated

* Enterprise Networking
* VLAN Segmentation
* FortiGate Administration
* FortiSwitch Administration
* Active Directory Integration
* IPSec VPN Configuration
* IDS Monitoring
* SPAN Configuration
* Network Security
* Traffic Visibility
* DMZ Design
* Cloud Integration
* Zero Trust Architecture
* Security Monitoring

---

## Network Summary

The SOC Homelab Enterprise network was designed to simulate a realistic enterprise security architecture using segmented VLANs, FortiGate security controls, FortiSwitch switching infrastructure, physical Suricata monitoring, Active Directory integration, cloud-connected telemetry, and dedicated attack simulation environments.

The architecture provides visibility across user, server, management, DMZ, cloud, and red team networks while supporting realistic SOC monitoring, detection engineering, incident investigation, and security operations workflows.

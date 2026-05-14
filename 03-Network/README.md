# Network Architecture

This section documents the network segmentation, VLAN design, firewall architecture, switching model, IDS visibility, and traffic monitoring implemented within the SOC Homelab Enterprise environment.

The objective was to simulate a realistic enterprise-style segmented security architecture with centralized visibility, secure routing, and IDS monitoring.

---

## Network Design Goals

The environment was designed to support:

- Enterprise network segmentation
- Secure routing
- DMZ isolation
- IDS visibility
- Traffic monitoring
- Attack simulation
- Secure management access
- Zero Trust principles
- Enterprise SOC workflows

---

## VLAN Architecture

The network is segmented into multiple security zones.

| VLAN | Network | Subnet | Purpose |
|------|----------|---------|----------|
| VLAN 10 | SOC_NET | 192.168.10.0/24 | SIEM and security tooling |
| VLAN 20 | USER_NET | 192.168.20.0/24 | User and attack simulation systems |
| VLAN 30 | SERVER_NET | 192.168.30.0/24 | Server infrastructure |
| VLAN 40 | MGMT_NET | 192.168.40.0/24 | Administrative management |
| VLAN 50 | DMZ_NET | 192.168.50.0/24 | Public-facing vulnerable applications |
| VLAN 60 | HOME_NET | Internal home network |
| VLAN 70 | GUEST_NET | Guest / isolated Wi-Fi |

---

## Core Network Components

### FortiGate 60F

Primary enterprise firewall responsible for:

- Inter-VLAN routing
- Security policy enforcement
- Firewall visibility
- VPN connectivity
- Network segmentation
- Administrative access

Primary management interface:

```text
192.168.40.1
```

---

### FortiSwitch 124E

Managed switch responsible for:

- VLAN switching
- Port segmentation
- SPAN mirroring
- IDS visibility
- Trunking

---

## SPAN / Port Mirroring Architecture

Traffic visibility is achieved using SPAN mirroring.

Mirror design:

```text
FortiGate Trunk (Port 1)
            +
Hyper-V Trunk (Port 7)
            ↓
SPAN Mirror
            ↓
Port 8
            ↓
Suricata IDS Sensor
```

This configuration provides:

- East-west visibility
- North-south visibility
- Inter-VLAN monitoring
- DMZ traffic monitoring
- Attack telemetry

---

## Security Zones

### SOC_NET (VLAN 10)

Purpose:

- SIEM infrastructure
- Security tooling
- Monitoring systems

Systems:

| Host | IP |
|------|----|
| WAZUH-01 | 192.168.10.10 |
| SPLUNK-01 | 192.168.10.20 |

---

### USER_NET (VLAN 20)

Purpose:

- User systems
- Attack simulation

Systems:

| Host | IP |
|------|----|
| WIN11-USER-01 | 192.168.20.10 |
| KALI-01 | 192.168.20.20 |

---

### SERVER_NET (VLAN 30)

Purpose:

- Identity services
- Server workloads

Systems:

| Host | IP |
|------|----|
| DC01 | 192.168.30.10 |
| DB01 | 192.168.30.20 |

---

### MGMT_NET (VLAN 40)

Purpose:

- Administrative access
- Infrastructure management

Systems:

| Host | IP |
|------|----|
| FortiGate Management | 192.168.40.1 |
| Mac Studio | 192.168.40.10 |

---

### DMZ_NET (VLAN 50)

Purpose:

- Vulnerable applications
- Web attack simulation

Systems:

| Host | IP |
|------|----|
| DVWA / WEB01 | 192.168.50.10 |
| Juice Shop | 192.168.50.20:3000 |

---

## IDS Visibility

### Physical Suricata Sensor

Suricata operates as a dedicated passive IDS sensor.

Capabilities include:

- HTTP monitoring
- DNS visibility
- TLS metadata
- JA3 / JA4 fingerprints
- SQL Injection detection
- Recon visibility
- Attack telemetry

Traffic visibility includes:

- VLAN-tagged traffic
- Inter-VLAN routing
- DMZ attacks
- Web exploitation activity
- Attack simulation telemetry

---

## Zero Trust Design Principles

The network follows several security principles:

- Segmentation first
- Least privilege
- Controlled access
- Visibility-driven monitoring
- Isolated management
- Secure remote administration

---

## Skills Demonstrated

- Enterprise Networking
- VLAN Segmentation
- Firewall Administration
- IDS Monitoring
- SPAN Configuration
- Network Security
- Traffic Visibility
- DMZ Design
- Zero Trust Architecture
- Security Monitoring

---

## Network Summary

The SOC Homelab Enterprise network was designed to simulate a realistic enterprise segmented architecture with firewall visibility, VLAN separation, DMZ isolation, IDS monitoring, and secure administrative access.

The network continues to evolve as new attack simulations, detections, dashboards, and monitoring capabilities are added throughout the lab lifecycle.

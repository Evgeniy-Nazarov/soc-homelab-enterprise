# Network

This section documents the enterprise-style segmented network architecture of the SOC Homelab Enterprise environment.

The network is designed around VLAN segmentation, centralized routing through FortiGate, passive IDS monitoring, and controlled visibility between environments.

---

## Network Design Goals

- Build enterprise-style network segmentation
- Isolate production-style environments
- Simulate real SOC visibility
- Centralize routing and policy enforcement
- Support attack simulation safely
- Enable secure remote access

---

## Network Architecture Overview

The environment is segmented into dedicated VLANs to separate security infrastructure, endpoints, servers, management systems, vulnerable services, home devices, and guest access.

All inter-VLAN routing is centralized through the FortiGate 60F firewall.

Network visibility is achieved through SPAN (port mirroring) to a physical Suricata IDS sensor.

---

## VLAN Segmentation

| VLAN | Network | Subnet | Purpose |
|------|---------|---------|----------|
| VLAN 10 | SOC_NET | 192.168.10.0/24 | SOC infrastructure and SIEM systems |
| VLAN 20 | USER_NET | 192.168.20.0/24 | User workstation and attack simulation |
| VLAN 30 | SERVER_NET | 192.168.30.0/24 | Active Directory and server infrastructure |
| VLAN 40 | MGMT_NET | 192.168.40.0/24 | Administrative management network |
| VLAN 50 | DMZ_NET | 192.168.50.0/24 | Vulnerable web applications |
| VLAN 60 | HOME_NET | 192.168.60.0/24 | Home and media devices |
| VLAN 70 | GUEST_NET | 192.168.70.0/24 | Isolated guest Wi-Fi |

---

## Network Devices

### FortiGate 60F

Primary security gateway responsible for:

- Inter-VLAN routing
- Firewall policy enforcement
- VPN connectivity
- Internet access control
- AWS tunnel connectivity
- Network segmentation

Management IP:

```text
192.168.40.1
```

---

### FortiSwitch 124E

Managed Layer 2 switch responsible for:

- VLAN switching
- 802.1Q trunking
- SPAN / port mirroring
- Segmented access ports

Switch management is integrated into the segmented SOC architecture.

---

## SPAN / IDS Monitoring Design

Traffic visibility is provided through passive monitoring.

### SPAN Configuration

| Port | Purpose |
|------|----------|
| Port 1 | FortiGate trunk |
| Port 7 | Hyper-V trunk |
| Port 8 | Suricata SPAN destination |

Suricata receives mirrored traffic from:

- Inter-VLAN traffic
- User activity
- Server traffic
- DMZ activity
- Security telemetry
- Attack simulations

This design allows full network visibility without placing Suricata inline.

---

## Security Zones

### SOC_NET (VLAN 10)

Contains:

- WAZUH-01
- SPLUNK-01

Purpose:

- SIEM monitoring
- Detection engineering
- Alert visibility

---

### USER_NET (VLAN 20)

Contains:

- WIN11-USER-01
- KALI-01

Purpose:

- User simulation
- Attack generation
- Endpoint telemetry

---

### SERVER_NET (VLAN 30)

Contains:

- DC01
- DB01

Purpose:

- Identity services
- DNS
- Database infrastructure

---

### MGMT_NET (VLAN 40)

Contains:

- Mac Studio

Purpose:

- Administrative access
- Infrastructure management
- Security monitoring

---

### DMZ_NET (VLAN 50)

Contains:

- DVWA
- Juice Shop

Purpose:

- Attack simulation
- Detection engineering
- Web attack monitoring

---

### HOME_NET (VLAN 60)

Purpose:

- Home devices
- Media systems
- Non-lab traffic

---

### GUEST_NET (VLAN 70)

Purpose:

- Isolated Wi-Fi access
- Internet only
- No SOC access
- No management access
- Fully segmented

---

## Remote Connectivity

Remote administration is designed through:

```text
MacBook Pro
      ↓
WireGuard VPN
      ↓
AWS HUB
      ↓
IPsec Tunnel
      ↓
FortiGate 60F
      ↓
SOC Environment
```

This design enables secure remote access without exposing internal systems directly to the internet.

---

## Network Security Principles

The environment follows enterprise security principles:

- Network segmentation
- Least privilege access
- Centralized routing
- Passive monitoring
- Secure remote access
- Traffic visibility
- Isolated guest access
- Controlled attack simulation

---

## Network Summary

The network architecture was designed to simulate a realistic enterprise SOC environment with segmented infrastructure, centralized control, passive IDS monitoring, and secure remote administration.

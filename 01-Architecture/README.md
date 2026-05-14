# Architecture

This section documents the high-level architecture of the SOC Homelab Enterprise project, including network segmentation, security zones, traffic visibility, SIEM architecture, cloud connectivity, and detection workflow.

## Architecture Goals

- Build an enterprise-style segmented SOC environment
- Separate SOC, user, server, management, DMZ, home, and guest networks
- Route and control inter-VLAN traffic through FortiGate
- Monitor mirrored network traffic with a physical Suricata IDS sensor
- Ingest telemetry into Splunk Enterprise and Wazuh XDR
- Support remote access through AWS HUB and VPN connectivity
- Maintain a clean, documented, portfolio-ready security architecture

## Core Architecture Components

| Component | Role |
|----------|------|
| FortiGate 60F | Firewall, routing, segmentation, VPN |
| FortiSwitch 124E | Managed switching, VLAN trunking, SPAN |
| Suricata IDS | Passive network monitoring through SPAN |
| Splunk Enterprise | Primary SIEM, dashboards, analytics |
| Wazuh XDR | Secondary SIEM/XDR, alerting, correlation |
| Active Directory | Identity and Windows domain services |
| Sysmon | Windows endpoint telemetry |
| AWS HUB | Cloud VPN hub and remote access point |
| Hyper-V | Virtualization platform for lab systems |

## Network Zones

| VLAN | Network | Purpose |
|------|---------|---------|
| VLAN 10 | SOC_NET | SIEM and SOC infrastructure |
| VLAN 20 | USER_NET | User workstation and attack simulation |
| VLAN 30 | SERVER_NET | Active Directory, DNS, database services |
| VLAN 40 | MGMT_NET | Management workstation and admin access |
| VLAN 50 | DMZ_NET | Vulnerable web applications |
| VLAN 60 | HOME_NET | Home and media devices |
| VLAN 70 | GUEST_NET | Isolated guest Wi-Fi, internet only |

## Monitoring Design

Network visibility is provided by a physical Suricata IDS sensor connected to a FortiSwitch SPAN destination port.

The sensor receives mirrored VLAN-tagged traffic and forwards security telemetry into:

- Splunk Enterprise
- Wazuh XDR

This design allows the lab to simulate real SOC monitoring workflows without placing the IDS inline.

## Detection Workflow

The core detection workflow is:

```text
Attack Simulation
        ↓
Network Traffic
        ↓
Suricata IDS
        ↓
Splunk / Wazuh
        ↓
Detection / Alert
        ↓
Dashboard / Investigation
        ↓
Documentation
```
## Current Architecture Diagram

![SOC Homelab Topology](soc-homelab-topology.png)

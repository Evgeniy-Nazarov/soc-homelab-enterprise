# Architecture

This section documents the high-level architecture of the SOC Homelab Enterprise project, including network segmentation, security zones, traffic visibility, SIEM architecture, cloud integration, and security monitoring workflows.

## Architecture Goals

- Build an enterprise-style segmented SOC environment
- Separate SOC, user, server, management, DMZ, home, guest, and red team networks
- Route and control inter-VLAN traffic through FortiGate 60F
- Monitor mirrored network traffic using a dedicated physical Suricata IDS sensor
- Centralize security telemetry in Splunk Enterprise and Wazuh XDR
- Support cloud connectivity and remote monitoring through AWS integration
- Simulate real-world SOC analyst workflows, investigations, and detections
- Maintain a documented, portfolio-ready enterprise security architecture

## Core Architecture Components

| Component | Role |
|----------|------|
| FortiGate 60F | Firewall, VLAN routing, segmentation, VPN connectivity |
| FortiSwitch 124E | Managed switching, VLAN trunking, SPAN configuration |
| Physical Suricata Sensor | Passive IDS monitoring of mirrored network traffic |
| Splunk Enterprise | Primary SIEM, log analysis, dashboards, investigations |
| Wazuh XDR | Endpoint monitoring, alerting, correlation, threat detection |
| Active Directory | Identity, authentication, DNS, DHCP, Group Policy |
| Sysmon | Advanced Windows endpoint telemetry |
| AWS HUB | Cloud integration, remote monitoring, VPN connectivity |
| Hyper-V | Virtualization platform hosting lab infrastructure |

## Network Zones

| VLAN | Network | Purpose |
|------|---------|---------|
| VLAN 10 | SOC_NET | SIEM, monitoring, and SOC infrastructure |
| VLAN 20 | USER_NET | Domain-joined user workstations |
| VLAN 30 | SERVER_NET | Active Directory, DNS, DHCP, and server infrastructure |
| VLAN 40 | MGMT_NET | Administrative management systems |
| VLAN 50 | DMZ_NET | Public-facing and vulnerable web applications |
| VLAN 60 | HOME_NET | Home and family devices |
| VLAN 70 | GUEST_WIFI | Isolated guest wireless network |
| VLAN 80 | RED_TEAM | Attack simulation and adversary systems |

## Monitoring Design

Network visibility is provided by a dedicated physical Suricata IDS sensor connected to a FortiSwitch SPAN destination port.

The sensor receives mirrored VLAN-tagged traffic from multiple security zones and forwards telemetry to:

- Splunk Enterprise
- Wazuh XDR

This architecture enables passive network monitoring without introducing inline latency or affecting production traffic.

## Detection Workflow

The core security monitoring workflow is:

```text
Attack Simulation
        ↓
Network Traffic
        ↓
FortiGate / FortiSwitch
        ↓
SPAN Port
        ↓
Physical Suricata Sensor
        ↓
Splunk Enterprise / Wazuh XDR
        ↓
Detection & Alerting
        ↓
Investigation & Analysis
        ↓
Documentation & Reporting
```

## Current Architecture Diagram

![SOC Homelab Topology](soc-homelab-topology.png)

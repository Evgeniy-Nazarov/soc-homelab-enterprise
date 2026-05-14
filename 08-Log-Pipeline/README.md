# Log Pipeline

This section documents the telemetry flow, log collection architecture, and detection pipeline used in the SOC Homelab Enterprise environment.

The goal is to simulate enterprise-style security visibility across endpoints, network traffic, IDS telemetry, firewall logs, and cloud-connected systems.

---

## Log Pipeline Objectives

- Centralize security telemetry
- Simulate real-world SIEM ingestion
- Enable detection engineering
- Support incident investigations
- Correlate endpoint and network activity
- Build blue-team visibility

---

## Telemetry Architecture

The lab collects telemetry from multiple layers:

```text
Endpoints / Servers
        ↓
Sysmon / Windows Logs
        ↓
Splunk + Wazuh

Network Traffic
        ↓
FortiGate + Suricata IDS
        ↓
Splunk + Wazuh

Cloud Infrastructure
        ↓
AWS HUB Logs
        ↓
Splunk + Wazuh
```

---

## Primary Log Sources

| Source | Type | Destination |
|--------|------|-------------|
| Sysmon | Endpoint telemetry | Splunk + Wazuh |
| Windows Event Logs | Endpoint security logs | Splunk + Wazuh |
| Suricata IDS | Network telemetry | Splunk + Wazuh |
| FortiGate | Firewall & network logs | Splunk + Wazuh |
| AWS HUB | Cloud logs | Splunk |
| Active Directory | Identity & authentication | Splunk + Wazuh |

---

## Endpoint Telemetry

### Sysmon

Sysmon is deployed on Windows systems to provide deep endpoint visibility.

Monitored telemetry includes:

- Process creation
- Parent-child process relationships
- Network connections
- PowerShell activity
- Persistence mechanisms
- Registry modifications
- LOLBins activity
- DNS queries
- WMI activity
- Named pipes

### Windows Hosts

| Host | Role |
|------|------|
| WIN11-USER-01 | User workstation telemetry |
| DC01 | Active Directory telemetry |

---

## Suricata IDS Pipeline

Suricata operates as a physical passive IDS sensor using SPAN monitoring.

Detection flow:

```text
Network Traffic
        ↓
FortiSwitch SPAN
        ↓
Suricata IDS
        ↓
EVE JSON
        ↓
Splunk + Wazuh
        ↓
Alert / Dashboard / Investigation
```

Collected telemetry includes:

- HTTP requests
- DNS activity
- TLS metadata
- JA3 / JA4 fingerprints
- Network flows
- SQL injection activity
- IDS alerts
- Scanning activity
- Brute-force attempts

---

## Splunk Log Ingestion

Splunk Enterprise functions as the **Primary SIEM** platform.

Primary responsibilities:

- Centralized log ingestion
- Security dashboards
- Detection engineering
- Timeline reconstruction
- Alert correlation
- Threat visibility
- MITRE ATT&CK mapping

Example log sources:

- Sysmon
- Windows Events
- Suricata EVE JSON
- FortiGate logs
- AWS telemetry

---

## Wazuh XDR Pipeline

Wazuh functions as a **Secondary SIEM / XDR platform**.

Primary responsibilities:

- Alerting
- Event correlation
- Endpoint monitoring
- Rule-based detections
- Security visibility
- Incident support

Wazuh receives telemetry from:

- Suricata IDS
- Sysmon
- Windows logs
- Authentication logs
- Active Directory activity

---

## FortiGate Logging

FortiGate provides:

- Firewall traffic logs
- Inter-VLAN visibility
- VPN events
- Security policy logs
- Administrative events

Forwarded to:

```text
FortiGate
      ↓
Splunk Enterprise
      ↓
Wazuh XDR
```

---

## AWS HUB Telemetry

AWS infrastructure supports:

- Secure remote connectivity
- VPN visibility
- Cloud-based access

Telemetry is forwarded into the SOC environment for visibility and monitoring.

---

## Example Detection Flow

SQL Injection Simulation:

```text
KALI-01
      ↓
Juice Shop / DVWA
      ↓
Suricata Detection
      ↓
EVE JSON
      ↓
Splunk / Wazuh
      ↓
Dashboard / Alert
      ↓
Incident Investigation
```

---

## Log Visibility Goals

The pipeline is designed to provide visibility into:

- Endpoint activity
- Authentication behavior
- Network attacks
- Web exploitation
- Threat simulations
- Administrative activity
- Security telemetry
- Cloud connectivity

---

## Current Pipeline Status

| Component | Status |
|-----------|--------|
| Sysmon → Splunk | ✅ Operational |
| Sysmon → Wazuh | ✅ Operational |
| Suricata → Splunk | ✅ Operational |
| Suricata → Wazuh | ✅ Operational |
| FortiGate → Splunk | ✅ Operational |
| FortiGate → Wazuh | ✅ Operational |
| AWS HUB → Splunk | ✅ Operational |
| Active Directory Logs | ✅ Operational |
| Detection Correlation | ✅ Active |

## Skills Demonstrated

- SIEM Engineering
- Detection Engineering
- Telemetry Correlation
- Log Pipeline Design
- IDS Monitoring
- Firewall Telemetry
- Endpoint Visibility
- Security Monitoring
- Threat Detection
- SOC Operations
- Windows Telemetry Analysis
- Cloud Security Visibility

## Pipeline Summary

The SOC Homelab Enterprise log pipeline combines endpoint telemetry, IDS monitoring, firewall visibility, cloud telemetry, and SIEM correlation to simulate enterprise-style SOC monitoring workflows.

The architecture enables realistic detection engineering, telemetry validation, attack visibility, and incident monitoring across network, endpoint, authentication, and cloud-connected systems.

This pipeline continues to evolve as additional detections, telemetry sources, dashboards, and investigation workflows are added throughout the lab lifecycle.

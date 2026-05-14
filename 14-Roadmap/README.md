# Roadmap

This section documents the evolution, milestones, completed phases, and future development plans for the SOC Homelab Enterprise environment.

The lab is built incrementally to simulate a realistic enterprise SOC with practical blue-team workflows, detection engineering, SIEM monitoring, and incident investigations.

---

## Completed Milestones

### Phase 1 — Core Infrastructure

Completed:

- Hyper-V environment deployment
- Windows Server 2022 installation
- Initial virtualization setup
- Core network deployment

Status:

```text
Completed
```

---

### Phase 2 — Enterprise Segmentation

Completed:

- VLAN segmentation
- SOC network isolation
- USER / SERVER / MGMT separation
- DMZ deployment
- HOME / GUEST separation

Status:

```text
Completed
```

---

### Phase 3 — Firewall & Switching Migration

Completed:

### pfSense → FortiGate 60F

- Firewall migration
- Improved stability
- Better routing visibility
- Enterprise policy control

### TP-Link → FortiSwitch 124E

- Managed switching
- VLAN trunking
- SPAN integration
- Improved monitoring

Status:

```text
Completed
```

---

### Phase 4 — SIEM Deployment

Completed:

### Splunk Enterprise

- Primary SIEM deployment
- Dashboard creation
- Log ingestion
- Security monitoring

### Wazuh XDR

- Secondary SIEM deployment
- Endpoint monitoring
- Alert visibility
- Correlation support

Status:

```text
Completed
```

---

### Phase 5 — IDS Monitoring

Completed:

### Suricata IDS

- Physical sensor deployment
- SPAN monitoring
- EVE JSON telemetry
- Splunk ingestion
- Wazuh ingestion

Status:

```text
Completed
```

---

### Phase 6 — Endpoint Visibility

Completed:

### Sysmon Deployment

- Windows telemetry
- Process monitoring
- PowerShell visibility
- Network connections
- Registry monitoring
- Endpoint detection

Status:

```text
Completed
```

---

### Phase 7 — Attack Simulation Environment

Completed:

### Vulnerable Applications

- DVWA deployment
- OWASP Juice Shop deployment
- DMZ integration
- Web attack testing

Status:

```text
Completed
```

---

## Current Focus

Active priorities:

- GitHub portfolio documentation
- Detection engineering documentation
- Dashboard documentation
- SOC workflow documentation
- Incident investigation writeups
- Attack simulation documentation

Status:

```text
In Progress
```

---

## Upcoming Development

### Detection Engineering

Planned:

- SQL Injection detections
- Nmap detection
- Brute-force detections
- PowerShell detections
- Authentication detections

---

### Incident Investigations

Planned:

- Cydeo SOC ticket investigations
- Timeline reconstruction
- IOC analysis
- Root cause analysis
- Case documentation

---

### Dashboard Improvements

Planned:

- MITRE ATT&CK mapping
- Threat timelines
- Attack correlation
- SOC KPI visibility
- Detection dashboards

---

### Remote Access

Planned:

- Full WireGuard implementation
- Secure external administration
- AWS HUB optimization

---

### Future Improvements

Potential future enhancements:

- Threat hunting workflows
- Additional attack simulations
- Detection tuning
- Advanced SIEM correlation
- Expanded dashboard visibility
- Additional endpoint telemetry

---

## Long-Term Goal

Build a realistic enterprise-style SOC environment capable of demonstrating:

- Detection engineering
- Incident response
- SIEM operations
- Threat monitoring
- Windows security
- IDS monitoring
- Cloud-connected security workflows

The environment is designed to support continuous learning, portfolio development, and preparation for SOC analyst roles.

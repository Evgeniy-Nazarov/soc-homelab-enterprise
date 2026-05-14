# SOC Lab Evolution

This document outlines the evolution of the SOC Homelab Enterprise environment, including major architectural decisions, infrastructure changes, troubleshooting lessons, migrations, and engineering improvements made throughout the development process.

The purpose of this document is to demonstrate continuous improvement, infrastructure maturity, troubleshooting methodology, and enterprise-focused security engineering practices.

---

# Phase 1 — Initial Lab Foundation

The initial environment focused on learning core SOC concepts, virtualization, network visibility, and SIEM monitoring.

Initial goals included:

- Building a practical SOC environment
- Learning SIEM workflows
- Building detection visibility
- Creating attack simulation capability
- Improving cybersecurity skills

Early infrastructure included:

- Hyper-V virtualization
- Windows Server
- Initial VLAN segmentation
- pfSense firewall
- TP-Link managed switch
- Virtual Suricata IDS
- QRadar testing
- Wazuh deployment

---

# Phase 2 — Early Network Architecture

### Initial Firewall Platform

The environment initially used:

```text
pfSense
```

Goals:

- VLAN routing
- Segmentation
- Firewall visibility
- Internet connectivity

Challenges encountered:

- Network instability
- Random connectivity interruptions
- Reduced reliability during long uptime
- Administrative complexity

Engineering decision:

```text
pfSense → FortiGate 60F
```

Reason for migration:

- Better enterprise visibility
- Greater stability
- Enterprise firewall workflows
- Improved routing reliability
- Better long-term scalability

Results:

- Stable connectivity
- Improved performance
- Better segmentation
- Enterprise administration experience

---

# Phase 3 — Network Switching Evolution

### Initial Switching Platform

The environment originally used:

```text
TP-Link Smart Switch
```

Challenges:

- Limited enterprise features
- Limited SPAN visibility
- Less flexible segmentation
- Reduced monitoring capability

Engineering decision:

```text
TP-Link → FortiSwitch 124E
```

Reasons:

- Enterprise switching
- Better VLAN visibility
- SPAN monitoring
- Improved segmentation
- Better IDS visibility

Results:

- Stable VLAN architecture
- Reliable port mirroring
- Better IDS telemetry
- Enterprise switching experience

---

# Phase 4 — IDS Monitoring Evolution

### Virtual IDS Phase

Suricata originally operated as:

```text
Virtual Machine IDS
```

Traffic monitoring relied on:

```text
Hyper-V mirror ports
```

Challenges:

- Inconsistent packet visibility
- Mirroring limitations
- Reduced monitoring reliability
- Limited visibility across VLANs

Engineering decision:

```text
Virtual Suricata → Physical Suricata Sensor
```

Architecture:

```text
FortiGate Trunk + Hyper-V Trunk
              ↓
        SPAN / Mirror
              ↓
      Physical Suricata Sensor
```

Reasons:

- Better packet visibility
- Stable monitoring
- Enterprise-style IDS design
- VLAN traffic monitoring
- Improved attack telemetry

Results:

- Reliable packet capture
- SQL Injection visibility
- JA3 / JA4 fingerprints
- Better attack detection
- DMZ traffic visibility

---

# Phase 5 — SIEM Evolution

### QRadar Phase

The environment initially included:

```text
QRadar Community Edition
```

Challenges:

- High resource requirements
- Increased complexity
- Limited practicality for the lab

Engineering decision:

```text
QRadar → Splunk + Wazuh
```

Reasons:

- Better flexibility
- More practical learning
- Dashboard customization
- Better detection engineering
- Enterprise market relevance

Results:

- Improved visibility
- Better dashboards
- Faster troubleshooting
- Better SOC workflow simulation

---

# Phase 6 — Dashboard Evolution

Early dashboards focused primarily on:

- Basic visibility
- Raw telemetry
- Log validation

Later improvements included:

- MITRE ATT&CK mapping
- Kill chain stages
- Threat severity
- SQL Injection monitoring
- Attack paths
- AWS administration visibility
- Timeline reconstruction
- Threat prioritization

Results:

- Better SOC visibility
- Realistic monitoring workflows
- Portfolio-quality dashboards

---

# Phase 7 — Cloud Integration

Cloud connectivity was added through:

```text
AWS HUB
```

Purpose:

- Secure remote administration
- VPN connectivity
- WireGuard access
- IPsec connectivity
- External SOC visibility

Architecture:

```text
MacBook Pro
      ↓
WireGuard VPN
      ↓
AWS HUB
      ↓
IPsec Tunnel
      ↓
FortiGate
      ↓
SOC Environment
```

Results:

- Secure remote access
- Cloud-connected SOC workflows
- Enterprise-style administration

---

# Phase 8 — Current Environment

Current architecture includes:

### Security Infrastructure

- Splunk Enterprise
- Wazuh XDR
- Suricata IDS (Physical Sensor)
- FortiGate 60F
- FortiSwitch 124E

### Endpoint Infrastructure

- Windows 11
- Sysmon
- Active Directory
- Windows Server 2022

### Attack Simulation

- Kali Linux
- DVWA
- OWASP Juice Shop

### Cloud & Remote Access

- AWS HUB
- WireGuard
- IPsec VPN

---

# Major Lessons Learned

Key engineering lessons:

- Stability matters more than complexity
- Physical IDS visibility improved detection quality
- Enterprise segmentation improves realism
- Detection engineering requires tuning
- Dashboards evolve through iteration
- Documentation improves learning
- Troubleshooting drives architecture maturity

---

# Final Outcome

The environment evolved from a learning-focused cybersecurity lab into a realistic enterprise-style SOC architecture capable of supporting:

- SIEM Engineering
- Detection Engineering
- Threat Monitoring
- IDS Visibility
- Incident Investigations
- Attack Simulation
- Cloud-connected Administration
- SOC Analyst Development

The lab continues to evolve through new detections, dashboards, investigations, attack simulations, and enterprise security engineering improvements.

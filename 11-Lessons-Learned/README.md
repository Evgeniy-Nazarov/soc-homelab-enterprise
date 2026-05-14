# Lessons Learned

This section documents technical challenges, failures, troubleshooting, migrations, architectural decisions, and engineering lessons learned while building the SOC Homelab Enterprise environment.

A major goal of this project is not only to build infrastructure, but also to document mistakes, limitations, and problem-solving processes.

---

## Major Infrastructure Lessons

### Firewall Migration

### pfSense → FortiGate 60F

Challenge:

- Network instability
- Random connectivity issues
- Reduced reliability

Solution:

- Migrated to FortiGate 60F
- Redesigned segmentation model
- Improved VLAN stability

Result:

- Stable infrastructure
- Better routing visibility
- Enterprise-style firewall management

---

### Switch Migration

### TP-Link → FortiSwitch 124E

Challenge:

- Limited enterprise visibility
- Restricted SPAN capabilities
- Less granular VLAN management

Solution:

- Migrated to FortiSwitch 124E
- Integrated SPAN monitoring
- Improved segmentation

Result:

- Better network visibility
- Reliable port mirroring
- Improved IDS architecture

---

## Suricata IDS Lessons

### Virtual IDS → Physical IDS

Challenge:

Virtual IDS monitoring through Hyper-V had limitations in traffic visibility and monitoring reliability.

Solution:

- Migrated to dedicated physical Suricata sensor
- Implemented SPAN monitoring
- Added dedicated SOC management interface

Result:

- Better traffic visibility
- Stable packet capture
- Enterprise-style IDS monitoring

---

### Wi-Fi Management → Dedicated SOC VLAN

Challenge:

Initial sensor management relied on temporary Wi-Fi access.

Solution:

- Added dedicated USB Ethernet adapter
- Connected sensor directly into SOC_NET
- Removed dependency on guest Wi-Fi

Result:

- Cleaner architecture
- Better management access
- Improved segmentation

---

## Detection Engineering Lessons

### SQL Injection Detection Challenges

Challenge:

Suricata ET SQL Injection signatures did not consistently trigger during OWASP Juice Shop testing.

Observed payloads included:

```text
' OR 1=1--
OR SLEEP(5)--
UNION SELECT
```

Root Cause:

- Some ET SQLi rules were disabled
- Signature coverage limitations
- Detection logic not optimized for observed payloads

Solution:

- Built custom Splunk detections
- Used HTTP URL visibility
- Tuned detection logic

Result:

- Successful high-severity SQL Injection alert
- Improved detection visibility
- Better telemetry understanding

---

### SPAN Duplicate Traffic

Challenge:

SPAN traffic caused duplicate visibility across mirrored VLAN traffic.

Observed issue:

Attack events appeared duplicated.

Solution:

Implemented:

```spl
dc(flow_id)
```

to deduplicate network events.

Result:

- Accurate attack counting
- Cleaner dashboard visibility
- Reduced duplicate telemetry

---

## SIEM Engineering Lessons

### Wazuh JSON Parsing

Challenge:

Suricata EVE JSON produced excessive fields for Wazuh parsing.

Solution:

- Built normalized pipeline
- Filtered event types
- Reduced noisy telemetry

Result:

- Cleaner ingestion
- Better alert visibility
- Improved parsing reliability

---

### Splunk Visibility Improvements

Challenge:

Raw telemetry initially lacked clarity.

Solution:

- Built custom dashboards
- Improved parsing
- Enhanced visibility

Result:

- Better SOC visibility
- Improved investigations
- Clear attack timelines

---

## Engineering Philosophy

Key lessons learned while building the environment:

- Stability matters more than complexity
- Visibility is more important than volume
- Detection engineering requires tuning
- Infrastructure evolves through troubleshooting
- Documentation improves long-term learning
- Enterprise segmentation improves security

---

## Summary

The SOC Homelab Enterprise environment evolved through multiple iterations, troubleshooting efforts, migrations, and engineering decisions.

Each failure and redesign contributed to a more realistic enterprise SOC architecture and stronger practical security engineering experience.

# SQL Injection Attack Simulation

## Objective

The objective of this simulation was to emulate a real-world SQL Injection attack against intentionally vulnerable web applications hosted in the SOC Homelab Enterprise environment.

The goal was to validate:

- Network visibility
- IDS monitoring
- EVE JSON telemetry generation
- SIEM log ingestion
- Detection engineering opportunities
- Dashboard visibility across the SOC stack

---

## Lab Environment

| Component | Value |
|------------|--------|
| Attacker | KALI-01 (192.168.20.20) |
| Targets | DVWA (192.168.50.10), Juice Shop (192.168.50.20) |
| IDS | Physical Suricata Sensor |
| SIEM | Splunk Enterprise + Wazuh |
| Network Visibility | FortiSwitch SPAN / Mirror Port |

---

## Attack Scenario

SQL Injection attacks were executed from the Kali Linux attack workstation against intentionally vulnerable web applications deployed inside the DMZ network.

The objective of the simulation was to validate:

- Web application attack visibility
- Suricata network telemetry
- EVE JSON log generation
- Splunk searchable events
- Wazuh alert visibility
- Detection engineering opportunities

Attack traffic traversed the segmented network and was observed through the FortiSwitch SPAN configuration feeding the physical Suricata sensor.

---

## Attack Flow

```text
KALI-01 (192.168.20.20)
        ↓
Juice Shop / DVWA
        ↓
FortiSwitch SPAN
        ↓
Physical Suricata Sensor
        ↓
EVE JSON
        ↓
Splunk + Wazuh
        ↓
Detection & Dashboard Visibility
```

---

## Payloads Used

The following SQL Injection payloads were tested during the simulation:

```sql
' OR 1=1--
OR SLEEP(5)--
UNION SELECT
```

These payloads were executed against vulnerable search and authentication functionality in Juice Shop and DVWA to generate realistic web attack telemetry.

---

## Telemetry Observed

The attack generated real telemetry across the SOC monitoring stack.

Observed artifacts included:

- HTTP requests containing URL-encoded SQL Injection payloads
- Source and destination IP visibility
- HTTP URL logging
- User-Agent visibility
- VLAN-tagged traffic visibility
- EVE JSON telemetry from Suricata
- Splunk searchable events
- Wazuh alert ingestion

### Example Observed Traffic

```text
Source IP:      192.168.20.20 (KALI-01)
Destination:    192.168.50.20 (Juice Shop)
Protocol:       HTTP
Attack Type:    SQL Injection

Example Payload:
/rest/products/search?q=%27%20OR%201%3D1--
```

---

## Detection Challenges

During testing, default Emerging Threats (ET) SQL Injection signatures did not consistently trigger for all attack variations.

### Findings

- Some SQL Injection response rules were disabled or commented
- URL-encoded payloads reduced signature reliability
- Generic SQL Injection signatures did not consistently detect all requests
- Time-based and encoded payloads generated telemetry without reliable alerting

This created an opportunity to improve visibility through custom detection engineering using network telemetry and SIEM correlation.

---

## Detection Improvements

To improve SQL Injection visibility, custom detection logic was developed using Splunk searches and network telemetry.

### Engineering Improvements

- HTTP URL monitoring
- Source and destination IP correlation
- Payload visibility analysis
- URL-encoded request inspection
- Flow deduplication using `dc(flow_id)`

This approach significantly improved attack visibility and enabled more reliable SQL Injection detection across the SOC monitoring environment.

---

## MITRE ATT&CK Mapping

| Technique | Description |
|------------|-------------|
| T1190 | Exploit Public-Facing Application |

The attack simulation aligns with **MITRE ATT&CK T1190 — Exploit Public-Facing Application**, commonly associated with web application exploitation and initial access attempts.

---

## Lessons Learned

Key lessons from this simulation included:

- Signature-based detection alone is insufficient
- Detection engineering is required to improve visibility
- URL encoding can reduce detection effectiveness
- SPAN visibility provided reliable telemetry across VLANs
- Splunk and Wazuh correlation improved investigation capability
- Real attack simulations provide valuable SOC engineering experience

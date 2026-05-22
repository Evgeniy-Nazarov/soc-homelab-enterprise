# Hydra Brute Force Attack Simulation

## Objective

The objective of this simulation was to emulate a real-world brute force attack against a vulnerable web application hosted inside the SOC Homelab Enterprise environment.

The goal of the exercise was to validate:

- Network visibility
- IDS monitoring
- HTTP authentication telemetry
- EVE JSON generation
- SIEM log ingestion
- Detection engineering opportunities
- Dashboard visibility across the SOC stack

---

## Lab Environment

| Component | Value |
|------------|--------|
| Attacker | KALI-01 (192.168.20.20) |
| Target | DVWA (192.168.50.10) |
| Attack Type | Brute Force Authentication Attack |
| Tool Used | Hydra |
| IDS | Physical Suricata Sensor |
| SIEM | Splunk Enterprise + Wazuh |
| Network Visibility | FortiSwitch SPAN / Mirror Port |

---

## Attack Scenario

A brute force authentication attack was executed from the Kali Linux attack workstation against the DVWA login page hosted in the DMZ network.

The objective of the simulation was to validate:

- Web authentication attack visibility
- HTTP login telemetry
- Suricata network monitoring
- EVE JSON event generation
- Splunk detection engineering
- Wazuh alerting capability
- MITRE ATT&CK alignment

The attack traversed the segmented network infrastructure and was observed through the FortiSwitch SPAN configuration feeding the physical Suricata sensor.

---

## Attack Flow

```text
KALI-01 (192.168.20.20)
        ↓
Hydra Brute Force Attack
        ↓
DVWA Login Portal
        ↓
FortiSwitch SPAN
        ↓
Physical Suricata Sensor
        ↓
EVE JSON Telemetry
        ↓
Splunk + Wazuh
        ↓
Detection & Investigation
```

---

## Attack Command Used

Hydra was used to generate brute force authentication traffic against the DVWA login page.

Command executed:

```bash
hydra -I -l admin -P /usr/share/wordlists/rockyou.txt 192.168.50.10 http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:F=Login failed"
```

---

## Telemetry Observed

The attack generated observable telemetry across the SOC monitoring environment.

Observed artifacts included:

- HTTP POST authentication attempts
- Source and destination IP visibility
- Login URL visibility
- User-Agent detection
- VLAN-tagged traffic visibility
- Flow tracking
- EVE JSON telemetry generation
- Splunk searchable events
- Wazuh custom alert generation

---

## Example Observed Traffic

| Field | Value |
|--------|--------|
| Source IP | 192.168.20.20 (KALI-01) |
| Destination IP | 192.168.50.10 (DVWA) |
| Protocol | HTTP |
| Method | POST |
| URL | `/dvwa/login.php` |
| User-Agent | `Mozilla/5.0 (Hydra)` |
| Attack Type | Brute Force Authentication |

---

## Detection Engineering

### Splunk Detection

A custom Splunk detection was developed to identify Hydra brute force activity based on HTTP telemetry.

Detection logic:

- Hydra User-Agent monitoring
- Login endpoint monitoring
- Source → Destination correlation
- Flow deduplication using `dc(flow_id)`
- VLAN visibility tracking

Splunk detection query:

```spl
host="SURICATA-01" sourcetype="suricata:eve"
event_type="http"
http_user_agent="*Hydra*"
dest_ip="192.168.50.10"
http_url="/dvwa/login.php"
| eval detection_name="Hydra Brute Force Detected"
| eval mitre_technique="T1110 - Brute Force"
| stats dc(flow_id) as unique_attempts values(http_user_agent) as user_agent values(vlan) as vlan by src_ip dest_ip detection_name mitre_technique
| sort - unique_attempts
```

---

### Wazuh Detection

A custom Wazuh rule was created to detect Hydra brute force activity based on HTTP telemetry.

Custom Rule ID:

```text
100710
```

Detection logic:

- HTTP login page monitoring
- Hydra User-Agent detection
- Login endpoint correlation
- MITRE ATT&CK mapping

Rule behavior:

- Rule Level: 10
- MITRE Technique: T1110 — Brute Force
- MITRE Tactic: Credential Access

---

## Detection Challenges

Default Suricata IDS signatures did not generate native alerts for Hydra brute force activity.

### Findings

- Hydra generated HTTP telemetry but not IDS alerts
- No default Suricata rule matched Hydra User-Agent behavior
- Brute force activity appeared as standard HTTP traffic
- Detection required custom SIEM correlation logic

This created an opportunity for detection engineering using network telemetry and SIEM-based correlation.

---

## MITRE ATT&CK Mapping

| Technique | Description |
|------------|-------------|
| T1110 | Brute Force |

The attack simulation aligns with MITRE ATT&CK **T1110 — Brute Force**, commonly associated with password guessing and credential access attempts.

---

## Screenshots

### Splunk Detection Evidence

![Hydra Splunk Detection](https://raw.githubusercontent.com/Evgeniy-Nazarov/soc-homelab-enterprise/main/05-Attack-Simulations/screenshots/hydra/hydra-bruteforce-detection-splunk.png)

### Wazuh Detection Evidence

![Hydra Wazuh Detection](https://raw.githubusercontent.com/Evgeniy-Nazarov/soc-homelab-enterprise/main/05-Attack-Simulations/screenshots/hydra/wazuh-hydra-bruteforce-detection.png)

---

## Lessons Learned

Key lessons from this simulation included:

- Signature-based IDS visibility alone is insufficient
- Detection engineering significantly improves attack visibility
- Hydra User-Agent telemetry provides strong detection opportunities
- SPAN visibility enabled reliable attack observation
- Splunk and Wazuh correlation improved investigation capability
- Custom SIEM detections increased monitoring effectiveness
- Real attack simulations provide valuable SOC engineering experience

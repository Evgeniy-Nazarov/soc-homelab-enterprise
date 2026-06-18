# Lessons Learned

This section documents technical challenges, troubleshooting efforts, infrastructure migrations, architectural decisions, and engineering lessons learned while building the SOC Homelab Enterprise environment.

One of the primary goals of this project is not only to build infrastructure, but also to document failures, root cause analysis, troubleshooting methodologies, and design decisions encountered throughout the build process.

---

## Infrastructure Evolution

### Firewall Migration

### pfSense → FortiGate 60F

Challenge:

The original environment was built around pfSense. As the lab expanded, network management became increasingly complex and troubleshooting consumed significant time.

Issues encountered:

* Network instability
* Routing inconsistencies
* Increased management overhead
* Limited enterprise feature parity

Solution:

* Migrated perimeter security to FortiGate 60F
* Rebuilt firewall policies
* Redesigned VLAN architecture
* Implemented enterprise-style segmentation

Result:

* Improved stability
* Simplified administration
* Better visibility
* Enterprise-grade firewall experience

---

### Switch Migration

### TP-Link → FortiSwitch 124E

Challenge:

The original switch infrastructure limited visibility and SPAN capabilities required for network monitoring.

Solution:

* Migrated to FortiSwitch 124E
* Implemented enterprise VLAN architecture
* Integrated SPAN monitoring

Result:

* Improved traffic visibility
* Better VLAN management
* Reliable IDS monitoring

---

## Network Architecture Lessons

### VLAN Segmentation Redesign

Challenge:

As the environment expanded, combining attack systems and user systems within the same network reduced realism and limited segmentation.

Solution:

Created dedicated security zones:

* USER_NET
* SERVER_NET
* SOC_NET
* MGMT_NET
* DMZ_NET
* HOME_NET
* GUEST_NET
* RED_TEAM

Result:

* Improved enterprise realism
* Better attack isolation
* More realistic monitoring scenarios
* Improved security architecture

---

### Application Layer Segmentation

Challenge:

Initially the DVWA application and backend database resided within the same security zone.

Solution:

Separated architecture into:

* DVWA Web Application → DMZ_NET
* Database Server (DB01) → SERVER_NET

Result:

* Simulated real-world multi-tier architecture
* Improved segmentation
* Better visibility into application-to-database communications

---

## IDS Engineering Lessons

### Virtual IDS → Physical IDS Migration

Challenge:

Initial Suricata deployments within Hyper-V experienced limitations in traffic visibility and packet monitoring reliability.

Solution:

* Built dedicated physical Suricata sensor
* Implemented FortiSwitch SPAN monitoring
* Added dedicated management connectivity

Result:

* Improved packet visibility
* Reliable monitoring
* Enterprise-style IDS deployment

---

### SPAN Duplicate Traffic

Challenge:

Mirrored traffic generated duplicate network events.

Observed behavior:

* Duplicate attack events
* Inflated event counts
* Dashboard inaccuracies

Solution:

Implemented event deduplication using:

```spl
dc(flow_id)
```

Result:

* Accurate event counts
* Cleaner dashboards
* Improved reporting accuracy

---

## Detection Engineering Lessons

### SQL Injection Detection Tuning

Challenge:

Default Suricata SQL Injection signatures did not consistently trigger during OWASP Juice Shop and DVWA testing.

Observed payloads included:

```text
' OR 1=1--
UNION SELECT
OR SLEEP(5)
```

Root Cause:

* Signature limitations
* Detection coverage gaps
* Application-specific behavior

Solution:

* Created custom detections
* Tuned alert logic
* Built additional Splunk correlation searches

Result:

* Reliable SQL Injection detection
* Improved telemetry understanding
* Better attack visibility

---

### Hydra Brute Force Detection

Challenge:

Initial Hydra brute force testing generated traffic but did not trigger meaningful alerts.

Root Cause:

* Missing detection logic
* Generic Suricata visibility

Solution:

* Built custom Wazuh detection rules
* Created custom alert logic
* Integrated MITRE ATT&CK mapping

Result:

* Reliable brute-force detection
* Better investigation workflows
* Improved detection engineering experience

---

## SIEM Engineering Lessons

### Splunk Data Summary Issue

Challenge:

Hosts appeared to stop updating within Splunk Data Summary despite logs continuing to ingest successfully.

Observed behavior:

* Hosts displayed outdated timestamps
* Event counts appeared incorrect
* Searches still returned current data

Root Cause:

Splunk host metadata became stale while underlying indexes remained healthy.

Solution:

* Investigated host metadata
* Validated index ingestion
* Rebuilt metadata visibility

Result:

* Accurate host reporting
* Improved understanding of Splunk metadata behavior
* Better troubleshooting methodology

---

### Suricata Log Normalization

Challenge:

Raw EVE JSON events generated excessive fields and inconsistent visibility.

Solution:

* Normalized event ingestion
* Reduced noise
* Filtered unnecessary telemetry

Result:

* Cleaner dashboards
* Better detections
* Easier investigations

---

## Cloud Integration Lessons

### AWS-HUB IPSec Troubleshooting

Challenge:

AWS-HUB unexpectedly stopped forwarding telemetry to Splunk.

Observed behavior:

* Splunk Universal Forwarder inactive
* Connectivity failures
* Tunnel appeared partially operational

Root Cause:

Multiple duplicate IPSec Security Associations caused routing and traffic flow inconsistencies.

Solution:

* Performed IPSec troubleshooting
* Analyzed VPN selectors
* Reviewed StrongSwan configuration
* Corrected IPSec session handling
* Re-established cloud telemetry paths

Result:

* Restored Splunk connectivity
* Restored Wazuh connectivity
* Improved VPN troubleshooting experience
* Better understanding of IPSec and StrongSwan behavior

---

### AWS-HUB Monitoring Integration

Challenge:

Cloud infrastructure initially provided limited visibility.

Solution:

Integrated:

* Splunk Universal Forwarder
* Wazuh Agent
* IPSec monitoring

Result:

* Full cloud telemetry visibility
* Hybrid monitoring architecture
* Improved cloud security experience

---

## Engineering Philosophy

Several key lessons emerged throughout the project:

* Stability is more valuable than complexity
* Visibility is more important than log volume
* Detection engineering requires continuous tuning
* Troubleshooting creates the most valuable learning experiences
* Segmentation improves both security and monitoring
* Documentation is as important as implementation
* Enterprise architecture evolves through iteration

---

## Skills Developed

* Infrastructure Troubleshooting
* Network Segmentation
* FortiGate Administration
* FortiSwitch Administration
* IPSec VPN Troubleshooting
* Linux Administration
* Active Directory Administration
* Splunk Administration
* Wazuh Administration
* IDS Engineering
* Detection Engineering
* SIEM Engineering
* Cloud Security Monitoring
* Incident Investigation
* Root Cause Analysis

---

## Lessons Learned Summary

The SOC Homelab Enterprise environment evolved through multiple redesigns, migrations, troubleshooting efforts, and architectural improvements.

Each technical challenge contributed to a deeper understanding of enterprise networking, cloud connectivity, security monitoring, detection engineering, and SOC operations.

The resulting environment reflects not only successful implementations, but also the practical troubleshooting and problem-solving experience required to operate and maintain enterprise security infrastructure.

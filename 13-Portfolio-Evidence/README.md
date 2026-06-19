# Portfolio Evidence

## Overview

This section highlights the practical security engineering, SOC operations, detection engineering, incident response, network security, and security monitoring capabilities demonstrated through the SOC Homelab Enterprise project.

The environment was designed to simulate enterprise security operations by combining security monitoring, network defense, Active Directory administration, cloud integration, detection engineering, and attack simulation within a single operational platform.

The primary objective is not simply tool deployment, but the implementation, operation, monitoring, troubleshooting, validation, and documentation of real-world security workflows commonly performed by SOC Analysts and Security Operations teams.

---

## Enterprise Security Architecture

Designed and implemented an enterprise-style security architecture using FortiGate and FortiSwitch infrastructure.

### Core Security Components

* FortiGate 60F Next-Generation Firewall
* FortiSwitch 124E Managed Switch
* Physical Suricata IDS Sensor
* Splunk Enterprise
* Wazuh XDR Platform
* Active Directory
* AWS Cloud Integration
* Site-to-Site IPsec VPN Connectivity

### Security Zones

| Security Zone | Purpose                                      |
| ------------- | -------------------------------------------- |
| SOC_NET       | Security Monitoring Infrastructure           |
| USER_NET      | Corporate Endpoints                          |
| SERVER_NET    | Active Directory and Infrastructure Services |
| MGMT_NET      | Administrative Management Network            |
| DMZ_NET       | Vulnerable Web Applications                  |
| HOME_NET      | Trusted Personal Devices                     |
| GUEST_WIFI    | Internet-Only Guest Wireless Network         |
| RED_TEAM      | Attack Simulation Environment                |

### Security Objectives

* Enterprise network segmentation
* East-West traffic control
* DMZ isolation
* SOC infrastructure isolation
* Secure cloud connectivity
* Centralized security monitoring
* Detection engineering validation
* Incident investigation support

---

## Security Monitoring Operations

Built and maintained a dual-SIEM architecture to provide centralized visibility across endpoints, servers, network infrastructure, IDS telemetry, and cloud resources.

### Security Platforms

| Platform          | Function                                  |
| ----------------- | ----------------------------------------- |
| Splunk Enterprise | Log Analytics and Security Monitoring     |
| Wazuh XDR         | Endpoint Visibility and Detection         |
| Suricata IDS      | Network Detection and Security Monitoring |
| Sysmon            | Advanced Windows Telemetry                |

### Telemetry Sources

* Windows Endpoints
* Windows Servers
* Active Directory
* Sysmon Events
* Suricata IDS
* FortiGate Firewall
* AWS Infrastructure
* Security Applications
* Network Traffic

### SIEM Engineering Activities

* Log onboarding
* Data source integration
* Event normalization
* Dashboard creation
* Alert validation
* Detection tuning
* Security monitoring workflows
* Cross-platform correlation

---

## Detection Engineering

Developed and validated detection content using network, endpoint, and application telemetry.

### Detection Engineering Activities

* Custom rule development
* SQL Injection detection
* IDS alert validation
* Alert tuning
* False positive reduction
* Detection troubleshooting
* MITRE ATT&CK mapping
* Security telemetry validation

### Detection Workflow

* Generate attack activity
* Capture telemetry
* Validate IDS visibility
* Confirm SIEM ingestion
* Tune detections
* Validate alerts
* Document findings

---

## Network Security Monitoring

Implemented a dedicated physical Suricata IDS sensor connected through a FortiSwitch SPAN port.

Unlike virtual-only monitoring environments, this deployment provides full packet visibility using mirrored network traffic from the switching infrastructure.

### Monitoring Capabilities

* Full packet visibility
* Network IDS monitoring
* Security telemetry collection
* Detection validation
* Attack simulation monitoring
* Network forensic visibility
* Security event generation

### Security Monitoring Flow

FortiSwitch SPAN Port → Physical Suricata Sensor → Splunk Enterprise + Wazuh XDR

---

## Firewall Engineering

Designed and implemented security controls using FortiGate 60F.

### Firewall Administration Experience

* VLAN routing
* Security policy implementation
* Access control management
* Network segmentation
* Address object management
* Service object creation
* Traffic monitoring
* Security policy troubleshooting
* VPN administration

### Custom Security Services

Implemented custom service objects for:

* WAZUH_AGENT
* WAZUH_WEB
* SPLUNK_UF
* SPLUNK_WEB
* JUICESHOP_3000
* MYSQL_3306

### Security Controls Implemented

* User-to-SOC access restrictions
* Server-to-SOC access restrictions
* DMZ isolation
* Database access control
* AWS secure connectivity
* Guest wireless isolation
* Red Team segmentation

---

## Active Directory Security Operations

Built and administered an enterprise-style Active Directory environment.

### Activities

* Domain administration
* Organizational Unit design
* Group Policy management
* Authentication monitoring
* User activity visibility
* Administrative auditing
* Security event analysis
* Endpoint integration

### Security Visibility

* Logon monitoring
* Administrative activity tracking
* Authentication auditing
* Endpoint telemetry collection
* Security event monitoring

---

## Endpoint Security Monitoring

Implemented endpoint visibility using Sysmon and Wazuh agents.

### Monitoring Capabilities

* Process creation monitoring
* PowerShell visibility
* User activity monitoring
* Authentication tracking
* Administrative action monitoring
* Security event collection
* Endpoint telemetry analysis

---

## Cloud Security Integration

Integrated AWS resources into the monitoring environment through secure site-to-site connectivity.

### AWS Security Components

* AWS EC2 Infrastructure
* AWS HUB Connectivity
* Site-to-Site IPsec VPN
* Cloud-connected Monitoring
* Hybrid Security Architecture

### Security Benefits

* Secure cloud connectivity
* Remote log collection
* Centralized visibility
* Cross-environment monitoring
* Hybrid SOC architecture

---

## Incident Investigation Experience

Performed investigations using telemetry collected from multiple security platforms.

### Investigation Activities

* Alert triage
* Event correlation
* IOC analysis
* Timeline reconstruction
* Threat hunting
* Log analysis
* Endpoint investigations
* Network investigations

### Investigation Data Sources

* Splunk Searches
* Wazuh Alerts
* Sysmon Events
* Suricata Alerts
* FortiGate Logs
* Active Directory Events

---

## Attack Simulation and Validation

Validated monitoring and detection capabilities through controlled attack simulations.

### Attack Scenarios

* SQL Injection
* Web Application Attacks
* Reconnaissance Activities
* Network Enumeration
* Detection Validation Exercises

### Target Systems

* OWASP Juice Shop
* DVWA (Damn Vulnerable Web Application)

### Objectives

* Validate visibility
* Verify telemetry collection
* Test detection coverage
* Improve alert quality
* Simulate adversary activity

---

## Documentation and Reporting

Produced detailed technical documentation covering architecture, monitoring, detection engineering, and security operations.

### Documentation Areas

* Security Architecture
* Network Segmentation
* FortiGate Administration
* SIEM Operations
* Detection Engineering
* Incident Investigations
* Attack Simulations
* Security Monitoring Workflows

---

## MITRE ATT&CK Exposure

Hands-on exposure to multiple ATT&CK tactics through attack simulation and detection validation activities.

### ATT&CK Areas

* TA0001 Initial Access
* TA0002 Execution
* TA0003 Persistence
* TA0005 Defense Evasion
* TA0006 Credential Access
* TA0007 Discovery
* TA0008 Lateral Movement
* TA0011 Command and Control
* TA0040 Impact

---

## Technologies Used

### Security Monitoring

* Splunk Enterprise
* Wazuh XDR
* Suricata IDS
* Sysmon

### Network Security

* FortiGate 60F
* FortiSwitch 124E
* VLAN Segmentation
* SPAN Port Monitoring
* Site-to-Site IPsec VPN

### Infrastructure

* Windows Server 2022
* Active Directory
* Hyper-V
* AWS EC2

### Operating Systems

* Windows Server 2022
* Windows 11
* Ubuntu Linux
* Kali Linux
* macOS

---

## Lessons Learned

Through the implementation and operation of this environment, several key security and operational lessons were reinforced:

* Effective network segmentation significantly reduces lateral movement opportunities.
* Security monitoring platforms require continuous validation and tuning.
* Centralized logging dramatically improves investigation efficiency.
* Physical IDS deployments provide valuable network visibility beyond endpoint telemetry.
* Cloud-connected infrastructure introduces additional monitoring and security considerations.
* Well-documented environments are easier to maintain, troubleshoot, and investigate.
* Detection engineering is an iterative process requiring ongoing validation and refinement.
* Practical attack simulation is one of the most effective methods for validating security controls and monitoring coverage.

---

## Portfolio Goal

This repository demonstrates practical, hands-on experience with enterprise security operations, SIEM administration, network security, detection engineering, cloud security integration, incident investigation, and SOC workflows.

The project was built to showcase the technical skills, operational knowledge, and security mindset expected of a modern SOC Analyst working within an enterprise environment.

---

## Summary

SOC Homelab Enterprise is a continuously evolving security environment designed to simulate real-world enterprise security operations.

The project combines FortiGate network security, Active Directory administration, Splunk and Wazuh monitoring, physical IDS deployment, AWS integration, detection engineering, and attack simulation into a unified platform that demonstrates practical blue-team experience and security operations capability.

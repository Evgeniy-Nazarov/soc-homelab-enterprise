# Active Directory

This section documents the Active Directory (AD) infrastructure used within the SOC Homelab Enterprise environment.

The goal is to simulate a realistic Windows enterprise identity environment for authentication monitoring, privilege management, endpoint telemetry, and incident investigation.

---

## Active Directory Objectives

- Simulate enterprise Windows infrastructure
- Centralize authentication
- Practice AD security monitoring
- Generate Windows telemetry
- Support detection engineering
- Monitor identity-based activity
- Build realistic blue-team scenarios

---

## Domain Infrastructure

### Domain Controller

| Hostname | IP Address | Role |
|----------|------------|------|
| DC01 | 192.168.30.10 | Active Directory Domain Controller |

Core services:

- Active Directory Domain Services (AD DS)
- DNS
- Authentication
- Group Policy
- Sysmon telemetry
- Security event logging

---

## Active Directory Network Placement

```text
SERVER_NET (VLAN 30)
192.168.30.0/24
```

Purpose:

- Isolated server infrastructure
- Identity services
- Authentication
- DNS management

Segmentation through VLAN 30 helps simulate enterprise-style infrastructure separation.

---

## Active Directory Groups

| Group | Purpose |
|--------|----------|
| Users | Standard user accounts |
| IT | Administrative IT operations |
| Support | Helpdesk / support staff |
| Admin | Domain administrators |

This structure simulates role-based access control (RBAC) commonly found in enterprise environments.

---

## Endpoint Integration

Connected Windows systems:

| Hostname | Role |
|----------|------|
| WIN11-USER-01 | Domain-joined workstation |
| DC01 | Domain controller |

Purpose:

- Authentication monitoring
- Group policy testing
- Windows event telemetry
- Privilege monitoring
- Endpoint detection

---

## Windows Telemetry

Telemetry is collected using:

### Sysmon

Monitored activity includes:

- Process creation
- PowerShell activity
- Parent-child process relationships
- Network connections
- Registry changes
- Persistence mechanisms
- LOLBins activity
- WMI activity
- Named pipes
- DNS queries

### Windows Event Logs

Collected events include:

- Successful logons
- Failed logons
- Account lockouts
- Privilege escalation
- Group membership changes
- Authentication failures
- Service creation
- Account modifications

---

## Authentication Visibility

Authentication telemetry flows into:

```text
Active Directory
        ↓
Windows Security Logs
        ↓
Sysmon
        ↓
Splunk + Wazuh
        ↓
Detection / Investigation
```

This enables visibility into:

- Login activity
- Failed authentication attempts
- Administrative actions
- User behavior
- Privileged account usage

---

## Example Monitoring Use Cases

Examples of monitored activity:

- Failed login attempts
- Privilege escalation
- Lateral movement simulation
- Suspicious PowerShell activity
- Administrative account usage
- Unauthorized group changes
- Persistence techniques

---

## Security Goals

The Active Directory environment supports:

- Identity monitoring
- Authentication analysis
- Detection engineering
- Incident investigations
- Privilege auditing
- Windows security telemetry
- Enterprise simulation

---

## Active Directory Summary

The Active Directory environment was built to simulate a realistic enterprise Windows domain with centralized authentication, endpoint telemetry, and identity-focused security monitoring for SOC analyst training and detection engineering practice.

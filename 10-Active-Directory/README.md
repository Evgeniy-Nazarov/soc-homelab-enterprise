# Active Directory

This section documents the Active Directory infrastructure implemented within the SOC Homelab Enterprise environment.

The goal is to simulate a realistic enterprise Windows domain that provides centralized authentication, identity management, endpoint administration, security monitoring, and telemetry generation for SOC operations, detection engineering, and incident investigation.

---

## Active Directory Objectives

The Active Directory environment was designed to:

* Simulate enterprise Windows infrastructure
* Centralize authentication and authorization
* Practice Active Directory administration
* Generate realistic Windows telemetry
* Support detection engineering
* Monitor identity-based activity
* Simulate enterprise security operations
* Create realistic SOC investigation scenarios

---

## Domain Environment

### Domain Information

| Component         | Value                |
| ----------------- | -------------------- |
| Domain Name       | SOCLAB.LOCAL         |
| Domain Controller | DC01                 |
| Domain Network    | SERVER_NET (VLAN 30) |
| Platform          | Windows Server 2022  |

The SOCLAB.LOCAL domain serves as the central identity provider for the lab environment and simulates a typical enterprise Active Directory deployment.

---

## Domain Controller

### DC01

| Hostname | IP Address    | Role                               |
| -------- | ------------- | ---------------------------------- |
| DC01     | 192.168.30.10 | Active Directory Domain Controller |

Core services provided by DC01:

* Active Directory Domain Services (AD DS)
* DNS Services
* DHCP Services
* Group Policy Management
* Centralized Authentication
* User and Computer Management
* Security Event Logging
* Sysmon Telemetry Collection

---

## Active Directory Network Placement

```text
SERVER_NET (VLAN 30)
192.168.30.0/24
```

Purpose:

* Identity services
* Authentication services
* Infrastructure services
* DNS management
* Centralized administration

Placing Active Directory within a dedicated server network simulates common enterprise segmentation practices.

---

## Organizational Structure

The domain includes dedicated Organizational Units (OUs) used for administration, policy management, and endpoint organization.

Example organizational structure:

```text
SOCLAB.LOCAL
│
├── 00_ADMIN
├── 01_SERVERS
├── 02_WORKSTATIONS
├── 03_USERS
├── 04_SERVICE_ACCOUNTS
├── 05_SECURITY
├── 06_SOC
└── 07_TEST_LAB
```

This structure supports scalable administration and enterprise-style policy management.

---

## Security Groups

Role-based access control is implemented through dedicated security groups.

| Group         | Purpose                           |
| ------------- | --------------------------------- |
| Domain Users  | Standard user accounts            |
| IT Support    | Administrative support operations |
| Security Team | Security monitoring activities    |
| Domain Admins | Domain administration             |
| SOC Team      | SOC administration and monitoring |

This structure simulates enterprise RBAC practices commonly used within production environments.

---

## Domain-Joined Systems

The Active Directory environment currently manages multiple Windows endpoints.

| Hostname      | IP Address    | Role                              |
| ------------- | ------------- | --------------------------------- |
| WIN11-USER-01 | 192.168.20.10 | Domain-Joined Windows 11 Endpoint |
| WIN11-USER-02 | 192.168.20.20 | Domain-Joined Windows 11 Endpoint |
| DC01          | 192.168.30.10 | Domain Controller                 |

All systems generate authentication, security, and endpoint telemetry that is forwarded to the monitoring platforms.

---

## Group Policy Configuration

The environment includes baseline security policies commonly found within enterprise environments.

Implemented controls include:

* Password complexity requirements
* Account lockout policies
* Password history enforcement
* Security auditing
* Authentication logging
* Administrative activity monitoring

These policies help generate realistic security events for monitoring and detection validation.

---

## Windows Telemetry Collection

Telemetry is collected through Sysmon and Windows Event Logging.

### Sysmon Visibility

Collected telemetry includes:

* Process creation
* Parent-child process relationships
* PowerShell activity
* Network connections
* Registry modifications
* Persistence mechanisms
* DNS queries
* WMI activity
* LOLBins execution
* Named pipe activity

### Windows Security Events

Collected events include:

* Successful logons
* Failed logons
* Account lockouts
* Privilege escalation
* Group membership changes
* User account modifications
* Service creation events
* Authentication failures
* Administrative activity

---

## Authentication Monitoring Pipeline

Authentication telemetry is integrated into the SOC monitoring architecture.

```text
Active Directory
        ↓
Windows Security Logs
        +
Sysmon
        ↓
Splunk Enterprise
        +
Wazuh XDR
        ↓
Detection / Investigation
```

This architecture provides visibility into:

* User authentication activity
* Failed login attempts
* Administrative actions
* Privileged account usage
* Identity-based attacks
* Authentication anomalies

---

## Example Monitoring Use Cases

The Active Directory environment supports detection and investigation of:

* Failed authentication attempts
* Password spraying simulations
* Privilege escalation activity
* Suspicious PowerShell execution
* Administrative account usage
* Unauthorized group membership changes
* Persistence mechanisms
* Lateral movement activity

---

## Security Monitoring Integration

### Splunk Enterprise

Used for:

* Authentication analysis
* Security investigations
* Timeline reconstruction
* Detection engineering
* Dashboard visualization

### Wazuh XDR

Used for:

* Endpoint monitoring
* Alerting
* Correlation rules
* Security visibility
* Incident response support

---

## Skills Demonstrated

* Active Directory Administration
* Windows Server Administration
* DNS Management
* DHCP Management
* Group Policy Administration
* Identity and Access Management
* Security Monitoring
* Authentication Analysis
* Sysmon Deployment
* Windows Event Analysis
* Detection Engineering
* SOC Operations

---

## Active Directory Summary

The Active Directory environment provides a centralized enterprise identity platform based on the SOCLAB.LOCAL domain. The infrastructure supports authentication services, policy management, endpoint administration, security monitoring, and telemetry generation across multiple domain-joined Windows systems.

The environment serves as the foundation for authentication monitoring, detection engineering, incident investigation, and enterprise SOC operations within the SOC Homelab Enterprise project.

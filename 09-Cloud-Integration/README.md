# Cloud Integration

This section documents the cloud-connected remote access architecture used in the SOC Homelab Enterprise environment.

The lab uses AWS infrastructure as a secure transport layer for remote SOC access, VPN connectivity, and controlled administrative access into the segmented lab environment.

---

## Cloud Integration Goals

- Support secure remote administration
- Simulate enterprise-style remote SOC access
- Avoid exposing internal systems directly to the internet
- Centralize secure ingress through cloud infrastructure
- Practice cloud-connected security architecture
- Maintain segmented and controlled access

---

## Cloud Architecture Overview

The environment uses AWS as a secure intermediate access layer.

Remote administration flow:

```text
MacBook Pro
      ↓
WireGuard VPN
      ↓
AWS HUB
      ↓
IPsec Tunnel
      ↓
FortiGate 60F
      ↓
SOC Homelab Environment
```

This model allows secure access into the SOC environment without exposing internal services publicly.

---

## AWS HUB

### Purpose

AWS HUB functions as:

- Secure cloud access point
- VPN transit layer
- Remote administration gateway
- Secure routing point
- External connectivity hub

---

### AWS Platform

| Component | Technology |
|-----------|-------------|
| Provider | AWS EC2 |
| OS | Ubuntu Server |
| Function | VPN HUB |
| Connectivity | WireGuard + IPsec |

---

## WireGuard VPN

WireGuard is used for:

- Secure remote access
- Encrypted connectivity
- Administrative access
- Secure communication

### Remote Access Model

Primary remote administration device:

| Device | Purpose |
|--------|---------|
| MacBook Pro (M1 Max) | Remote SOC administration |

Expected use cases:

- Hotel Wi-Fi
- Mobile hotspot
- Public internet
- External administration
- Incident response access

---

## IPsec Tunnel

IPsec provides secure site-to-site connectivity between:

```text
AWS HUB
      ↕
FortiGate 60F
```

Purpose:

- Secure tunnel transport
- Encrypted connectivity
- Controlled access into the lab
- Enterprise-style VPN simulation

---

## Security Design Principles

The cloud architecture follows:

- Zero Trust mindset
- Least privilege access
- No public exposure of internal systems
- Segmented infrastructure
- Encrypted communications
- Controlled ingress path

---

## Administrative Access Workflow

Administrative access flow:

```text
Remote MacBook
        ↓
WireGuard VPN
        ↓
AWS HUB
        ↓
IPsec Tunnel
        ↓
FortiGate Firewall
        ↓
SOC Environment
```

Access allows visibility into:

- Splunk dashboards
- Wazuh monitoring
- FortiGate administration
- SOC telemetry
- Infrastructure management

---

## Cloud Monitoring Visibility

Cloud-connected telemetry supports:

- VPN visibility
- Secure remote access monitoring
- Administrative activity
- Tunnel health validation
- Connectivity troubleshooting

---

## Cloud Integration Summary

The cloud integration architecture enables secure, enterprise-style remote access into the SOC Homelab Enterprise environment through AWS, WireGuard, and IPsec without exposing internal services directly to the internet.

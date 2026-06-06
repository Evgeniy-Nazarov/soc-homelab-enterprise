# PowerShell Process Injection Investigation

## Executive Summary

A CrowdStrike Falcon detection identified suspicious PowerShell activity associated with a potential Process Injection attack on a Windows Server 2022 endpoint.

The investigation revealed execution of a PowerShell script named `Start-Hollow.ps1`, a script commonly associated with Process Hollowing techniques used by adversaries to inject malicious code into legitimate processes.

CrowdStrike successfully detected and prevented execution before compromise could be confirmed.

---

## Incident Overview

| Field | Value |
|---------|---------|
| Investigation Type | Process Injection Investigation |
| Severity | High |
| Detection Source | CrowdStrike Falcon |
| Host | VMI1146645 |
| User | morgan |
| Status | Blocked / Contained |
| MITRE ATT&CK | T1055, T1059.001, T1105, T1071.001 |

---

## Detection Summary

CrowdStrike Falcon generated a high-severity detection indicating PowerShell-based Process Injection activity.

The investigation identified execution of:

```powershell
Start-Hollow.ps1
```

The script demonstrated behavior consistent with Process Hollowing and PowerShell-based malware execution.

Observed activity included:

- PowerShell ExecutionPolicy bypass
- Malicious script execution
- DNS communication to GitHub infrastructure
- Potential payload staging activity
- Process Injection behavior

---

## Evidence Collected

### CrowdStrike Script Execution Evidence

![CrowdStrike Script Execution Evidence](screenshots/powershell-process-injection/crowdstrike-script-execution-evidence.png)

CrowdStrike telemetry identified execution of a malicious PowerShell script during an active RDP session.

Observed behavior included:

- Execution of `DiskCleanupTask.ps1`
- Creation of `Start-Hollow.ps1`
- PowerShell ExecutionPolicy bypass
- User-driven execution activity

Assessment:

The activity is consistent with a PowerShell-based malware loader attempting to stage a Process Injection attack.

---

### VirusTotal Malware Analysis

![VirusTotal Malware Analysis](screenshots/powershell-process-injection/virustotal-malicious-powershell-analysis.png)

The recovered PowerShell script was analyzed using VirusTotal.

Results showed:

- 28 security vendors detected the file as malicious
- Multiple vendors classified the file as Trojan malware
- Detection names referenced Process Hollowing and PowerShell injection techniques

Assessment:

The file represents a high-confidence malicious PowerShell payload associated with process injection activity.

---

### Domain Reputation Verification

![Domain Reputation](screenshots/powershell-process-injection/virustotal-domain-reputation-check.png)

Investigation identified outbound communication involving:

```text
raw.githubusercontent.com
```

VirusTotal reputation analysis showed the domain itself is legitimate GitHub infrastructure.

Assessment:

Although the domain is trusted, GitHub content delivery infrastructure is frequently abused by threat actors to host malicious scripts and stage payload delivery.

The observed communication is consistent with malware retrieval activity.

---

### CrowdStrike DNS Request Evidence

![CrowdStrike DNS Request Evidence](screenshots/powershell-process-injection/crowdstrike-dns-request-evidence.png)

CrowdStrike recorded DNS activity to:

```text
raw.githubusercontent.com
```

Observed behavior included:

- DNS lookup request
- Outbound HTTPS connection attempt
- Communication during script execution

Assessment:

The endpoint attempted to retrieve content from external GitHub-hosted infrastructure during execution of the malicious PowerShell script.

---

## MITRE ATT&CK Mapping

| Technique ID | Technique |
|-------------|-----------|
| T1055 | Process Injection |
| T1059.001 | PowerShell |
| T1105 | Ingress Tool Transfer |
| T1071.001 | Web Protocols |

---

## Timeline

| Time | Event |
|--------|--------|
| 08:50 | User established RDP session |
| 08:53 | DiskCleanupTask.ps1 executed |
| 08:53 | Start-Hollow.ps1 created |
| 08:53 | DNS request to raw.githubusercontent.com |
| 08:53 | Outbound HTTPS communication initiated |
| 08:53 | CrowdStrike generated detection |
| 08:53 | Malicious script quarantined |
| 08:53 | Process Injection attempt blocked |

---

## Findings

The investigation confirmed execution of a malicious PowerShell script associated with Process Hollowing techniques.

Key findings:

- Malicious PowerShell script identified
- VirusTotal confirmed malicious reputation
- Process Injection behavior detected
- GitHub infrastructure used for payload staging
- DNS communication observed during execution
- CrowdStrike successfully blocked the attack
- No persistence mechanisms identified

---

## Conclusion

The alert was determined to be a true positive PowerShell-based Process Injection attempt.

The malicious script leveraged PowerShell ExecutionPolicy bypass techniques and attempted to retrieve content from GitHub-hosted infrastructure before initiating Process Injection activity.

CrowdStrike Falcon successfully detected, blocked, and quarantined the malicious script before successful compromise could be confirmed.

No evidence of persistence, additional payload execution, or lateral movement was identified following containment actions.

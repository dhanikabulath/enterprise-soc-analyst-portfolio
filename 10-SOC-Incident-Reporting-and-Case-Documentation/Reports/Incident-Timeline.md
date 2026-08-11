# Incident Timeline – Agent Tesla Malware Case

## Incident Overview

**Incident Type:** Malware Execution  
**Classification:** True Positive – Malware  
**Severity:** High  
**Malware Family:** Agent Tesla  
**Affected User:** admin  

## Timeline

| Stage | Event | Analyst Assessment |
|---|---|---|
| Detection | `agent_tesla.exe` identified in sandbox analysis | Suspicious executable submitted for investigation |
| Execution | Executable observed running as PID 3768 | Confirmed process execution |
| File Analysis | File observed executing from `C:\Users\admin\AppData\Local\Temp\agent_tesla.exe` | Execution from user Temp directory warranted investigation |
| Sandbox Analysis | ANY.RUN classified activity as malicious | Malware classification confirmed |
| Malware Identification | Sandbox identified Agent Tesla / stealer | Incident escalated as malware |
| IOC Extraction | SHA-256 extracted from sample | File IOC available for enterprise-wide hunting |
| Threat Intelligence | SHA-256 investigated using VirusTotal | Independent reputation evidence obtained |
| Network Review | Sandbox network telemetry reviewed | No C2 connection confidently attributable to the malware process |
| Scope Assessment | File hash identified for environment-wide hunting | Other endpoints should be searched for the IOC |
| Containment Decision | Endpoint isolation and file quarantine recommended | Containment required for a production incident |
| Eradication | Malware removal, persistence checks and endpoint scan recommended | Host integrity must be validated |
| Recovery | Restore endpoint to trusted state and monitor | Endpoint should return to service only after validation |
| Closure | Evidence documented and incident classified | True Positive – Malware |

## Confirmed IOC

```text
File: agent_tesla.exe

SHA256:
fdb7456a43bc3c0296c18043bf32f21b8a29d099f91fb690a6816d202d6ad51a
```

## Final Disposition

**True Positive – Malware**

The investigation confirmed malicious executable activity. Network command-and-control and credential theft were not established from the evidence reviewed and therefore were not recorded as confirmed incident behavior.
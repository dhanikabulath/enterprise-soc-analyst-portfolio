# Microsoft Defender XDR Investigation Report

## Incident Information

**Incident ID:** 4  
**Incident:** Execution incident on one endpoint  
**Severity:** Medium  
**Affected Endpoint:** DC01  
**Affected User:** Admin  
**Category:** Execution

## Executive Summary

Microsoft Defender XDR detected suspicious PowerShell activity on the Windows 11 endpoint `DC01`.

The activity generated two correlated alerts and was grouped into an XDR incident. Investigation of the process tree identified a chain from `userinit.exe` through `explorer.exe` and `cmd.exe` to `powershell.exe`.

The PowerShell command used execution-policy bypass, hidden execution, WebClient file-download functionality, and subsequent process execution.

The activity was intentionally generated as part of an authorized Microsoft Defender for Endpoint security test.

## Key Findings

- Defender for Endpoint successfully detected the simulated activity.
- Defender XDR created a Medium-severity incident.
- Two alerts were correlated into the incident.
- PowerShell was identified as suspicious.
- The complete parent-child process relationship was available for investigation.
- The command used `-ExecutionPolicy Bypass`.
- PowerShell was configured with `-WindowStyle Hidden`.
- `System.Net.WebClient.DownloadFile()` was present.
- `Start-Process` was used for subsequent execution.
- Defender associated process, IP, URL, endpoint, and user evidence with the incident.
- The activity was confirmed to be authorized security testing.

## Process Chain

```text
userinit.exe
    ↓
explorer.exe
    ↓
cmd.exe
    ↓
powershell.exe
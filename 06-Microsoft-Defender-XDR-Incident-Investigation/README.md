# Project 06 – Microsoft Defender XDR Incident Investigation

## Overview

This project demonstrates an endpoint security incident investigation using Microsoft Defender XDR and Microsoft Defender for Endpoint.

A controlled security test generated suspicious PowerShell activity on a Windows 11 endpoint. Microsoft Defender detected the activity, created alerts, and correlated them into an XDR incident.

The investigation followed the incident from initial detection through process analysis, evidence review, classification, and resolution.

## Environment

- Microsoft Defender XDR
- Microsoft Defender for Endpoint
- Windows 11
- Endpoint: `DC01`
- Incident ID: `4`
- Severity: Medium

## Investigation

### 1. Initial Detection

Microsoft Defender XDR generated an incident titled:

`Execution incident on one endpoint`

The incident contained a Medium-severity alert:

`Suspicious PowerShell command line`

![Initial Detection](Screenshots/01-Defender-XDR-Incident-Detected.png)

### 2. Process Tree Analysis

Defender reconstructed the process execution chain:

```text
userinit.exe
    ↓
explorer.exe
    ↓
cmd.exe
    ↓
powershell.exe
```

![Process Tree](Screenshots/02-Defender-XDR-Process-Tree.png)

### 3. PowerShell Process Investigation

The suspicious process was:

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

The executable itself was legitimate Windows PowerShell. The suspicious behavior resulted from how PowerShell was invoked.

![Process Details](Screenshots/03-Suspicious-PowerShell-Process-Details.png)

### 4. Command-Line Analysis

The detected command included:

```text
-NoExit
-ExecutionPolicy Bypass
-WindowStyle Hidden
```

It then used `System.Net.WebClient.DownloadFile()` and attempted to execute the resulting file using `Start-Process`.

![Command Line](Screenshots/04-Suspicious-PowerShell-Command-Line.png)

### 5. Endpoint Investigation

The affected Windows 11 endpoint was reviewed in Defender XDR. The device was active and had been assigned a Medium risk level following the detection.

![Endpoint](Screenshots/05-Affected-Endpoint-Overview.png)

### 6. XDR Incident Correlation

Defender XDR correlated the activity into Incident ID 4 and associated the endpoint, user, alerts, process activity, and network-related evidence.

![Attack Story](Screenshots/06-XDR-Incident-Attack-Story.png)

### 7. Evidence Review

The Evidence and Response view was reviewed for associated:

- Process evidence
- IP evidence
- URL evidence

![Evidence](Screenshots/07-Incident-Evidence-and-Response.png)

## Classification

The activity was intentionally generated as an authorized Microsoft Defender for Endpoint security test.

The alert was therefore classified as:

```text
Informational, expected activity
Security testing
```

It was not classified as a false positive because Defender correctly identified genuinely suspicious PowerShell behavior.

![Classification](Screenshots/08-Alert-Classification-Security-Testing.png)

The incident was subsequently documented and resolved.

![Incident Resolution](Screenshots/09-XDR-Incident-Classification-and-Resolution.png)

![Resolved Incident](Screenshots/10-Resolved-Defender-XDR-Incident.png)

## Analyst Verdict

**Authorized Security Testing – No Unauthorized Compromise Identified**

Microsoft Defender XDR successfully detected suspicious PowerShell execution and correlated the endpoint, identity, process, and related evidence into an investigation-ready incident.

## Skills Demonstrated

- Microsoft Defender XDR
- Microsoft Defender for Endpoint
- Endpoint Detection and Response (EDR)
- Alert triage
- XDR incident investigation
- Process tree analysis
- PowerShell investigation
- Command-line analysis
- Evidence analysis
- Incident classification
- Incident resolution
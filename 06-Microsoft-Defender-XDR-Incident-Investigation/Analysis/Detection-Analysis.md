# Detection Analysis

## Detection

**Alert:** Suspicious PowerShell command line  
**Severity:** Medium  
**Category:** Execution  
**Endpoint:** DC01  
**User:** DC01\Admin

## Process Chain

```text
userinit.exe
    ↓
explorer.exe
    ↓
cmd.exe
    ↓
powershell.exe
```

The process tree shows PowerShell being launched from `cmd.exe` during an interactive Windows session.

## Suspicious Command

```powershell
powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference='silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe','C:\test-WDATP-test\invoice.exe');Start-Process 'C:\test-WDATP-test\invoice.exe'
```

## Suspicious Characteristics

### Execution Policy Bypass

```text
-ExecutionPolicy Bypass
```

Attempts to execute PowerShell without normal execution-policy restrictions.

### Hidden Execution

```text
-WindowStyle Hidden
```

Requests execution with the PowerShell window hidden.

### Download Capability

```text
System.Net.WebClient.DownloadFile()
```

Uses PowerShell/.NET functionality capable of retrieving a file.

### Subsequent Execution

```text
Start-Process
```

Attempts to execute the downloaded file.

## Network Indicator

The command referenced:

```text
127.0.0.1
```

This is the local loopback address and is not an external malicious IOC in this investigation.

## Assessment

The combination of execution-policy bypass, hidden PowerShell execution, file retrieval, and subsequent process execution resembles behavior frequently investigated by SOC analysts.

In this case, however, the activity was deliberately generated as part of an authorized Microsoft Defender for Endpoint detection test.

The Defender alert was therefore valid, while the underlying activity was expected.

## Final Classification

```text
Informational, expected activity
Determination: Security testing
```
# Enterprise SOC Analyst Portfolio

A hands-on cybersecurity portfolio demonstrating practical Security Operations Center (SOC) skills across phishing analysis, SIEM monitoring, Windows security investigation, network forensics, web attack analysis, endpoint detection and response, threat hunting, threat intelligence, malware analysis, incident response, and professional security reporting.

The portfolio consists of **10 investigation-based projects** designed around common SOC analyst responsibilities.

---

## Portfolio Overview

| # | Project | Primary Skills / Tools |
|---|---|---|
| 01 | Phishing Email Investigation & IOC Analysis | Email analysis, header investigation, IOC extraction, VirusTotal, CyberChef |
| 02 | SIEM Detection & Alert Triage | Microsoft Sentinel, KQL, Log Analytics, alert investigation |
| 03 | Windows Event Log Hunting & Security Investigation | Windows Event Viewer, Sysmon, PowerShell, Windows Security Events |
| 04 | Network Attack Investigation | Wireshark, PCAP analysis, TCP/IP, DNS, HTTP, TLS |
| 05 | Web Application Attack Investigation | Log4Shell, JNDI, HTTP analysis, payload decoding, Wireshark |
| 06 | Microsoft Defender XDR Incident Investigation | Defender XDR, Defender for Endpoint, EDR, process-tree analysis |
| 07 | Identity Threat Hunting with Defender XDR | Advanced Hunting, KQL, Entra ID, authentication analysis |
| 08 | Threat Intelligence & IOC Enrichment | VirusTotal, AlienVault OTX, IOC enrichment, infrastructure correlation |
| 09 | Malware Analysis & Incident Response | ANY.RUN, VirusTotal, malware triage, IOC extraction, incident response |
| 10 | SOC Incident Reporting & Case Documentation | Technical reporting, executive reporting, incident timelines, remediation |

---

# Project 01 – Phishing Email Investigation & IOC Analysis

Investigated a suspicious email from a SOC analyst perspective.

The project focused on identifying indicators of phishing and determining whether URLs, domains, sender information, and other artifacts warranted escalation.

### Skills

- Email header analysis
- Sender investigation
- URL analysis
- IOC extraction
- Reputation analysis
- Phishing classification
- Analyst documentation

---

# Project 02 – SIEM Detection & Alert Triage

Built hands-on experience with **Microsoft Sentinel** and SIEM alert investigation.

Security telemetry was reviewed using Kusto Query Language (KQL), and alerts were analyzed from the perspective of a SOC analyst.

### Technologies

```text
Microsoft Sentinel
Azure Log Analytics
KQL
Microsoft Azure
```

### Skills

- SIEM investigation
- KQL querying
- Alert triage
- Security-event analysis
- Detection analysis
- Incident documentation

---

# Project 03 – Windows Event Log Hunting & Security Investigation

Investigated Windows security telemetry to identify potentially suspicious endpoint and authentication activity.

The project focused on understanding how Windows events can be used during SOC investigations.

### Technologies

```text
Windows Event Viewer
Windows Security Logs
Sysmon
PowerShell
```

### Skills

- Windows Event Log analysis
- Authentication-event investigation
- Process investigation
- Event correlation
- Endpoint security analysis

---

# Project 04 – Network Attack Investigation

Analyzed malicious network traffic using **Wireshark and PCAP evidence**.

The investigation examined multiple network protocols and identified suspicious communication patterns and infrastructure.

### Protocols Investigated

```text
TCP
DNS
HTTP
TLS
```

### Skills

- Wireshark
- PCAP investigation
- TCP stream analysis
- DNS analysis
- HTTP analysis
- TLS analysis
- Network IOC identification
- C2-related traffic investigation

The investigation identified infrastructure that was later used for threat-intelligence enrichment in Project 08.

---

# Project 05 – Web Application Attack Investigation

Investigated suspicious HTTP traffic associated with a **Log4Shell/JNDI exploitation attempt**.

The analysis included identification and decoding of an injected payload containing a JNDI LDAP reference and encoded command.

### Skills

- Web attack investigation
- HTTP request analysis
- Log4Shell analysis
- JNDI injection analysis
- Base64 decoding
- Payload analysis
- IOC extraction
- Network forensics

---

# Project 06 – Microsoft Defender XDR Incident Investigation

Investigated a controlled endpoint security incident using **Microsoft Defender XDR and Microsoft Defender for Endpoint**.

Defender detected suspicious PowerShell activity and correlated the endpoint telemetry into an XDR incident.

### Investigation Flow

```text
Detection
   ↓
Alert Triage
   ↓
Process Tree
   ↓
Command-Line Analysis
   ↓
Affected Endpoint
   ↓
Evidence Review
   ↓
Classification
   ↓
Resolution
```

### Skills

- Microsoft Defender XDR
- Microsoft Defender for Endpoint
- EDR investigation
- Process-tree analysis
- PowerShell investigation
- Command-line analysis
- Incident correlation
- Alert classification
- Incident resolution

---

# Project 07 – Identity Threat Hunting with Microsoft Defender XDR

Conducted proactive identity threat hunting using **Defender XDR Advanced Hunting and KQL**.

Unlike alert-driven investigation, this project started with a hunting hypothesis and queried raw authentication telemetry.

The hunt identified **48 failed authentication events** associated with a single account and source IP.

Further investigation examined:

```text
Affected account
      ↓
Source IP
      ↓
Authentication error codes
      ↓
Temporal clustering
      ↓
Successful vs failed authentication
      ↓
Application correlation
      ↓
Analyst assessment
```

47 of the 48 failures were concentrated within three hourly periods.

The activity was primarily associated with normal Microsoft applications, while the account also showed substantial successful authentication activity.

### Final Assessment

```text
Suspicious authentication pattern investigated.
Insufficient evidence of password spraying or malicious account compromise.
```

### Skills

- Microsoft Defender XDR
- Advanced Hunting
- KQL
- Microsoft Entra ID
- Identity threat hunting
- Authentication analysis
- Temporal analysis
- Hypothesis-driven investigation

---

# Project 08 – Threat Intelligence & IOC Enrichment

Performed threat-intelligence enrichment on suspicious infrastructure previously identified during network analysis.

Primary indicators included:

```text
45.131.214.85
vadusa.xyz
```

The indicators were investigated using multiple intelligence sources.

### Tools

```text
VirusTotal
AlienVault OTX
AbuseIPDB
Open-source threat intelligence
```

VirusTotal showed multiple malicious, malware, and suspicious classifications for the investigated IP.

AlienVault OTX provided associated URL intelligence and independently demonstrated an infrastructure relationship between:

```text
vadusa.xyz
      ↓
45.131.214.85
```

### Skills

- Threat intelligence
- IOC enrichment
- IP reputation analysis
- Domain analysis
- Passive infrastructure investigation
- Cross-source correlation
- Confidence assessment
- Defensive IOC recommendations

---

# Project 09 – Malware Analysis & Incident Response

Analyzed an **Agent Tesla** malware sample using an existing public ANY.RUN sandbox submission.

No malware was downloaded or executed locally.

### Confirmed Evidence

```text
Malware: Agent Tesla
File: agent_tesla.exe
User: admin
PID: 3768

Execution:
C:\Users\admin\AppData\Local\Temp\agent_tesla.exe
```

### SHA-256

```text
fdb7456a43bc3c0296c18043bf32f21b8a29d099f91fb690a6816d202d6ad51a
```

ANY.RUN classified the activity as malicious and identified Agent Tesla. The extracted hash was subsequently investigated using VirusTotal.

Network activity that could not be confidently attributed to the malware process was intentionally excluded from the confirmed IOC set.

### Incident Response

The investigation developed recommendations covering:

```text
Containment
     ↓
Environment-wide IOC hunting
     ↓
Eradication
     ↓
Credential-risk assessment
     ↓
Recovery
     ↓
Post-incident monitoring
```

### Skills

- Malware triage
- ANY.RUN sandbox analysis
- Process investigation
- File-hash analysis
- VirusTotal
- IOC extraction
- Incident classification
- Containment planning
- Eradication
- Recovery planning

---

# Project 10 – SOC Incident Reporting & Case Documentation

Converted technical investigation evidence from the Agent Tesla case into professional SOC documentation.

Three different reporting artifacts were developed:

```text
Incident Timeline
Technical Incident Report
Executive Incident Summary
```

The project demonstrates the ability to communicate the same security incident to different audiences.

### Technical Reporting

Documents:

- Confirmed evidence
- IOCs
- Process information
- Scope
- Containment
- Eradication
- Recovery

### Executive Reporting

Communicates:

- What happened
- Severity
- Potential business risk
- Required actions
- Final incident classification

### Evidence Handling

The reports explicitly distinguish between:

```text
CONFIRMED EVIDENCE
        vs
UNCONFIRMED MALWARE CAPABILITIES
```

This prevents known malware-family behavior from being incorrectly reported as activity observed during the specific investigation.

### Skills

- SOC incident reporting
- Technical security writing
- Executive communication
- Incident timeline development
- Evidence validation
- Severity assessment
- Remediation recommendations

---

# SOC Investigation Workflow Demonstrated

Across the ten projects, the portfolio demonstrates the broader SOC lifecycle:

```text
                     SECURITY EVENT
                           │
                           ▼
                       DETECTION
                           │
                           ▼
                        TRIAGE
                           │
                           ▼
                     INVESTIGATION
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
          Endpoint       Network       Identity
          Analysis       Analysis      Analysis
             │             │             │
             └─────────────┼─────────────┘
                           ▼
                    IOC IDENTIFICATION
                           │
                           ▼
                   THREAT INTELLIGENCE
                           │
                           ▼
                    SCOPE ASSESSMENT
                           │
                           ▼
                  INCIDENT RESPONSE
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
         Containment   Eradication   Recovery
              │            │            │
              └────────────┼────────────┘
                           ▼
                       REPORTING
```

---

# Technology Stack

## SIEM & Security Operations

```text
Microsoft Sentinel
Microsoft Defender XDR
Microsoft Defender for Endpoint
Azure Log Analytics
```

## Query & Scripting

```text
Kusto Query Language (KQL)
PowerShell
```

## Endpoint Security

```text
Windows 11
Windows Security Events
Sysmon
Microsoft Defender for Endpoint
```

## Network Security

```text
Wireshark
PCAP Analysis
TCP/IP
DNS
HTTP
TLS
```

## Threat Intelligence

```text
VirusTotal
AlienVault OTX
AbuseIPDB
```

## Malware Analysis

```text
ANY.RUN
VirusTotal
Static IOC Analysis
Sandbox Analysis
```

## Frameworks & Methodologies

```text
MITRE ATT&CK
IOC Analysis
Threat Hunting
Incident Response
SOC Alert Triage
```

---

# Core SOC Skills Demonstrated

- Alert triage
- SIEM investigation
- KQL querying
- Endpoint Detection and Response
- Windows security analysis
- Identity threat hunting
- Network traffic analysis
- PCAP investigation
- Phishing analysis
- Web attack investigation
- Threat intelligence
- IOC enrichment
- Malware triage
- Sandbox analysis
- Incident classification
- Incident response
- Evidence validation
- Technical incident reporting
- Executive security communication

---

# Portfolio Structure

```text
enterprise-soc-analyst-portfolio/
│
├── 01-Phishing-Email-Investigation/
│
├── 02-SIEM-Detection-and-Alert-Triage/
│
├── 03-Windows-Event-Log-Investigation/
│
├── 04-Network-Attack-Investigation/
│
├── 05-Web-Application-Attack-Investigation/
│
├── 06-Microsoft-Defender-XDR-Incident-Investigation/
│
├── 07-Identity-Threat-Hunting-with-Defender-XDR/
│
├── 08-Threat-Intelligence-and-IOC-Enrichment/
│
├── 09-Malware-Analysis-and-Incident-Response/
│
├── 10-SOC-Incident-Reporting-and-Case-Documentation/
│
└── README.md
```

---

## Portfolio Objective

The objective of this portfolio is to demonstrate practical capability for **Junior SOC Analyst / Security Operations Analyst roles** through investigation-based projects rather than tool demonstrations alone.

The projects progress from individual security-analysis tasks toward complete SOC workflows involving detection, investigation, threat hunting, intelligence enrichment, incident response, and professional reporting.


## 4. `PCAP/README.md`

```markdown
# PCAP Source

## Dataset

**Five Days of Server Traffic Including Log4j Attempts**

**Source:** Malware-Traffic-Analysis.net  
**Date:** December 2021

---

## Purpose

The PCAP was used for a SOC-style investigation of web application attack traffic, with a focus on Log4Shell/JNDI exploitation attempts.

The investigation included:

- HTTP traffic analysis
- JNDI payload identification
- Attack-source analysis
- Base64 decoding
- IOC extraction
- Threat-intelligence enrichment
- Exploitation validation
- MITRE ATT&CK mapping
- Incident reporting

---

## PCAP Handling

The original packet capture is not redistributed in this repository.

The repository contains only my investigation materials, screenshots, analysis, and reporting.

---

## Scope Limitation

The investigation is based on network evidence contained within the supplied PCAP.

Although Log4Shell exploitation attempts were clearly observed, no outbound connections to the primary attacker's specified LDAP or second-stage infrastructure were identified.

Successful exploitation therefore could not be confirmed from the available network evidence.
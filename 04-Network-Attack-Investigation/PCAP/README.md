# PCAP Source

## Exercise

**Easy As 123 – Traffic Analysis Exercise**

**Date:** 28 February 2026  
**Source:** Malware-Traffic-Analysis.net

---

## Purpose

The packet capture was used to perform a SOC-style network security investigation involving:

- Endpoint identification
- User identification
- DNS analysis
- HTTP analysis
- TCP stream analysis
- Remote-access traffic investigation
- IOC extraction
- Threat-intelligence enrichment
- MITRE ATT&CK mapping
- Incident reporting

---

## PCAP Handling

The original PCAP is **not redistributed in this repository**.

Only my investigation materials are included:

- Screenshots
- IOC analysis
- Incident report
- Investigation documentation

This keeps the repository focused on the analysis without redistributing the original exercise material.

---

## Investigation Environment

The packet capture was analyzed using:

- Wireshark
- VirusTotal
- MITRE ATT&CK

---

## Scope Limitation

The investigation is based on network traffic available in the supplied PCAP.

Conclusions are therefore limited to evidence observable within the packet capture.

The investigation identified suspicious NetSupport Manager remote-access communication, but the available network evidence did not establish the original infection vector or endpoint-level execution and persistence mechanisms.
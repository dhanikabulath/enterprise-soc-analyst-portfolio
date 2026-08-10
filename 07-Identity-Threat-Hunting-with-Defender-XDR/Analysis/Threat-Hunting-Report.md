# Identity Threat Hunting Report

## Investigation Objective

This threat hunt examined Microsoft Entra ID authentication telemetry for patterns potentially associated with:

- Password guessing
- Password spraying
- Unauthorized authentication attempts
- Account compromise
- Abnormal authentication behavior

The investigation was conducted using Microsoft Defender XDR Advanced Hunting.

## Data Source

```text
EntraIdSignInEvents
```

## Initial Finding

The hunt identified:

```text
Failed authentication events: 48
Affected accounts:              1
Observed source IPs:            1
```

Because the failures targeted only one account, the available evidence did not indicate a conventional password-spraying pattern across multiple accounts.

## Authentication Error Analysis

The following error-code distribution was identified:

| Error Code | Events |
|---|---:|
| 50126 | 23 |
| 50126 | 13 |
| 500133 | 6 |
| 50011 | 4 |
| 70008 | 1 |
| 50140 | 1 |

The presence of multiple error codes indicated that the failures were not represented as one uniform authentication failure condition in the hunting dataset.

## Successful Authentication Context

Authentication telemetry also showed:

```text
Affected account
Successful sign-ins: 1,903
Failed sign-ins:        48

Second observed account
Successful sign-ins:    27
```

The substantial volume of successful authentication was considered when assessing the failed events.

## Temporal Analysis

Failed authentication events were distributed as follows:

```text
Aug 7 – 12:00 hour     14
Aug 7 – 01:00 hour     13
Aug 7 – 02:00 hour     20
Aug 8 – 05:00 hour      1
```

A total of **47 of 48 failures** occurred within three hourly buckets on August 7.

This concentration was sufficiently unusual to justify further investigation.

## Application Correlation

The failures were associated with:

| Application | Failed Sign-ins |
|---|---:|
| Windows Search | 25 |
| Cascade Authentication | 7 |
| OfficeHome | 7 |
| Microsoft Office | 4 |
| Microsoft Edge-related applications | 4 |
| Azure Portal | 1 |

Windows Search generated 25 of the 48 observed failed events.

The concentration among Microsoft applications provided additional context suggesting that authentication/session behavior should be considered alongside malicious authentication hypotheses.

## Threat Assessment

### Password Spraying

**Not supported by the observed evidence.**

Password spraying normally involves authentication attempts against multiple accounts. Only one account was associated with the failed events in this dataset.

### Repeated Authentication Failures

**Observed.**

The affected account generated 48 failures, with 47 concentrated within three hourly periods.

### Multiple-source Authentication Attack

**Not observed.**

The investigated failures were associated with one source IP.

### Account Compromise

**Not established.**

The dataset contained substantial successful authentication activity for the same account, but the available evidence did not establish unauthorized access.

## Analyst Verdict

The hunt successfully identified a concentrated authentication anomaly requiring investigation.

Correlation across account, source, error code, time, application, and successful authentication volume did not provide sufficient evidence to classify the activity as password spraying or malicious account compromise.

The observed pattern is more consistent with an authentication, application, or session-related issue, although the precise root cause was not established from the available telemetry.

### Final Disposition

**Suspicious authentication activity investigated – insufficient evidence of malicious compromise.**
# KQL Threat Hunting Queries

## 1. Review Entra ID Sign-In Events

```kusto
EntraIdSignInEvents
| take 20
```

**Purpose:** Verify that Microsoft Entra ID authentication telemetry is available for threat hunting.

---

## 2. Identify Failed Sign-Ins

```kusto
EntraIdSignInEvents
| where ErrorCode != 0
| order by Timestamp desc
```

**Finding:** 48 failed authentication events were identified.

---

## 3. Failed Sign-Ins by Account

```kusto
EntraIdSignInEvents
| where ErrorCode != 0
| summarize FailedAttempts=count() by AccountUpn
| order by FailedAttempts desc
```

**Finding:** All 48 failures were associated with a single account.

This did not support a multi-account password-spraying pattern.

---

## 4. Failed Sign-Ins by Source IP

```kusto
EntraIdSignInEvents
| where ErrorCode != 0
| summarize FailedAttempts=count() by IPAddress
| order by FailedAttempts desc
```

**Finding:** The investigated failures originated from a single source IP.

The public IP was intentionally excluded from portfolio documentation.

---

## 5. Authentication Error-Code Analysis

```kusto
EntraIdSignInEvents
| where ErrorCode != 0
| summarize Count=count() by ErrorCode
| order by Count desc
```

**Finding:** Multiple authentication error codes were present, indicating that the failed events did not represent one uniform failure condition.

---

## 6. Successful vs Failed Sign-Ins

```kusto
EntraIdSignInEvents
| summarize
    SuccessfulSignIns=countif(ErrorCode == 0),
    FailedSignIns=countif(ErrorCode != 0)
    by AccountUpn
```

**Finding:**

```text
Affected account:
1,903 successful
48 failed

Second observed account:
27 successful
```

This provided additional context for evaluating the failed authentication activity.

---

## 7. Failed Authentication Timeline

```kusto
EntraIdSignInEvents
| where ErrorCode != 0
| summarize FailedSignIns=count() by bin(Timestamp, 1h)
| order by Timestamp asc
```

**Finding:**

```text
14 failures → Aug 7 hourly bucket
13 failures → Aug 7 hourly bucket
20 failures → Aug 7 hourly bucket
 1 failure  → Aug 8 hourly bucket
```

47 of 48 failures occurred within three hourly periods.

---

## 8. Failed Sign-Ins by Application

```kusto
EntraIdSignInEvents
| where ErrorCode != 0
| summarize FailedSignIns=count() by Application
| order by FailedSignIns desc
```

**Finding:**

```text
Windows Search              25
Cascade Authentication       7
OfficeHome                   7
Microsoft Office             4
Microsoft Edge-related       4
Azure Portal                 1
```

The application distribution was used to evaluate whether the authentication pattern was more consistent with malicious authentication attempts or application/session-related behavior.

---

## Hunting Conclusion

The KQL investigation progressed from broad authentication discovery to increasingly specific pivots:

```text
Authentication telemetry
        ↓
Failed sign-ins
        ↓
Affected accounts
        ↓
Source IP
        ↓
Error codes
        ↓
Successful vs failed activity
        ↓
Temporal clustering
        ↓
Application correlation
        ↓
Analyst assessment
```

The investigation identified suspicious clustered authentication failures but found insufficient evidence of password spraying or malicious account compromise.
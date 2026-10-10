# SOC-OPS-004 - Measured retrospective triage

## Session
- Start UTC: 2026-10-10T13:51:00.4501922Z
- End UTC: 2026-10-10T14:17:05.2072724Z
- Session elapsed seconds: 1564.76
- Effective working time: not measured
- Method: retrospective triage of Wazuh alerts

## Investigations
| Case | Wazuh rule | Alert ID | Elapsed triage seconds | Disposition |
|---|---|---|---:|---|
| TRIAGE-001 | 92058 | 1791640013.366353 | 124.62 | Likely benign, unconfirmed; handover |
| TRIAGE-002 | 61102 | 1791637724.356447 | 526.03 | Operational connectivity failure; root cause unconfirmed |

## Metrics
- Investigations measured: 2
- Mean triage elapsed seconds: 325.32
- Median triage elapsed seconds: 325.32
- Confirmed security incidents: none established
- End-to-end containment/recovery: not performed
- Queue-wide deduplication: not measured

## Findings
- Rule 92058: sdbinst.exe launched under SYSTEM with PcaSvc parent context. Exact operation provenance remains unverified.
- Rule 61102: Windows GroupPolicy Event ID 1129. DNS lookup, domain discovery, TCP 389 and TCP 445 checks failed against DC01 during investigation. Secure-channel test returned False.
- GroupPolicy Event ID 1500 was also observed. Current domain connectivity was not demonstrated.
- The rule 92058 alert timestamp precedes its Sysmon event timestamp by approximately 819 ms. Time-source consistency remains unverified.

## Limitations
- Triage values represent elapsed wall-clock time, not continuous active work.
- Only two investigated alerts; not representative of the entire queue.
- No unique incident counts or false-positive rates can be inferred.
- Raw source JSON requires sanitization before publication.
- No shared infrastructure was modified.

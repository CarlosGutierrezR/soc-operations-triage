# SOC-OPS-004 - Operational handover

## TRIAGE-001
- Rule: 92058
- Status: likely benign, unconfirmed
- Action: verify sdbinst.exe operation provenance and investigate timestamp discrepancy
- Containment: none

## TRIAGE-002
- Rule: 61102; Windows GroupPolicy Event ID 1129
- Status: operational connectivity failure, cause unconfirmed
- Target for follow-up: SOC CORE
- Observed failures: domain DNS resolution, DC discovery, TCP 389, TCP 445
- Secure channel: False while DC connectivity was unavailable
- Next action: verify DC01 power state, networking, DNS and relevant services
- Restriction: do not reset secure channel or reconfigure shared infrastructure without a separate approved change

## Remaining limitations
- Neither investigation establishes a confirmed malicious incident.
- No technical containment or recovery was performed.
- Queue-wide deduplication remains unverified.

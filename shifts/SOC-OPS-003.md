# SOC-OPS-003 — SOC Monitoring Session

## Session information

- Date: 2026-10-10
- Platform: Wazuh Threat Hunting
- Manager filter: soc-wazuh-01
- Session type: Interrupted monitoring and triage exercise
- Status: Initial review completed; handover documented

## Session timestamps

- Start UTC: 2026-10-10T10:50:50.7664302Z
- End UTC: 2026-10-10T12:51:11.2721167Z
- Elapsed time: 120.34 minutes
- Effective analyst working time: Not measured
- Individual alert triage time: Not measured

The elapsed time must not be interpreted as continuous analyst activity.

## Monitoring baseline

- Query: Last 24 hours
- Displayed window: 2026-10-09 14:44 to 2026-10-10 14:44
- Observed alert hits: 192
- Distinct incidents: Not determined
- Scope: Alerts matching the Wazuh manager filter

## Initial alert queue

| Rule ID | Level | Description | Initial priority |
| --- | --- | --- | --- |
| 92058 | 12 | Application Compatibility Database launched | High |
| 61102 | 5 | Windows System error event | Medium |
| 92052 | 4 | Windows command prompt started by an abnormal process | Medium |
| 61104 | 3 | Service startup type was changed | Medium-Low |
| 60608 | 4 | Summary event of the report's signatures | Low |

The table represents rule families visible in the screenshot,
not an exhaustive distribution of all 192 alert hits.

## Triage — Wazuh rule 92058

- Agent: WIN11-EP-01
- Source: Sysmon Event ID 1
- Event UTC: 2026-10-10 11:46:53.224
- Process: C:\Windows\System32\sdbinst.exe
- Command: sdbinst.exe -m -bg
- Parent: svchost.exe
- Parent service: PcaSvc
- Account: NT AUTHORITY\SYSTEM
- Signature status: Valid
- Exact certificate subject: Not captured
- MITRE ATT&CK: T1546.011
- Priority: High at initial triage
- Assessment: Likely legitimate Windows compatibility activity
- Confidence: Moderate-High
- Confirmed compromise: Not established
- Containment: Not performed
- Final disposition: Pending verification of operation provenance

## Investigation limitations

- The exact compatibility operation was not identified.
- A valid executable signature does not prove benign execution.
- Alert timestamp precedes the Sysmon event UTC timestamp;
  clock synchronization and processing timing were not validated.
- The original alert JSON has not been sanitized for publication.

## Operational metrics

- Observed alert hits: 192
- Rule families visible in the reviewed screenshot: 5
- Detailed alert investigations documented in this session: 1
- Confirmed incidents among investigated alerts: 0
- Effective monitoring duration: Not available
- Mean time to triage: Not available
- Mean time to respond: Not available

## Handover

- Review rule 61102 if additional Windows errors are observed.
- Group recurring 60608 and 61104 alerts before individual triage.
- Preserve rule 92058 as a provisional assessment.
- Do not suppress rules or modify detection logic without testing.
- Continue monitoring in a new, explicitly timed session.

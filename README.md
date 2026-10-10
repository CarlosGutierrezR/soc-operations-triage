# SOC Operations — Monitoring, Triage & Incident Response

## Operational problem
A SOC analyst must prioritize heterogeneous alerts, distinguish observed behavior from confirmed incidents, document decisions, and hand work over without equating SIEM hits with unique incidents.

## Scope and environment
This portfolio exercise uses the shared SOC Lab. Documented investigations use Wazuh alerts from `WIN11-EP-01` and Windows Sysmon process-creation telemetry. Network telemetry is in the intended scope, but this repository does not yet demonstrate network-to-host correlation.

## Observed outcomes
- `CASE-001`: Wazuh rule `92066` investigated; authorized closure as **Likely Benign — Closed with Residual Uncertainty**. Wazuh SCA initiation was not conclusively attributed.
- `SOC-OPS-002`: 101 Wazuh alert hits in a retrospective 24-hour filter; rule `92052` evaluated provisionally as Windows maintenance activity.
- `SOC-OPS-003`: 192 hits in a separate, moving 24-hour window; rule `92058` prioritized and investigated. Execution context was consistent with Windows application compatibility processing, but operation provenance and a timestamp discrepancy remain unresolved.
- No incident, false-positive rate, MTTA, MTTD or MTTR is claimed from the available records.

The 101 and 192 figures describe different observations of moving windows and **must not be added together** or interpreted as unique alerts, cases, or incidents.

## Operational workflow
Alert intake → prioritization → evidence review → hypothesis → disposition → escalation/closure → handover → feedback.

## Repository map
- `docs/SOC-OPS-001.md`: original scope (historical initial status; not a live status report).
- `docs/triage-procedure.md`: operational triage SOP.
- `docs/severity-model.md`: severity/priority decision policy.
- `docs/escalation-matrix.md`: response and escalation policy.
- `docs/limitations.md`: known constraints.
- `cases/CASE-001.md`: investigated and administratively closed case.
- `cases/CASE-002.md`: initial assessment of `sdbinst.exe` from SOC-OPS-003; remains open/inconclusive.
- `shifts/SOC-OPS-002.md`, `shifts/SOC-OPS-003.md`: retrospective baseline and interrupted shift.
- `shifts/handover-001.md`: actionable handover.
- `metrics/case-register.csv`: traceable case-level records, with missing time fields left empty.
- `metrics/observations.csv`: aggregate observations kept separate from individual case metrics.
- `evidence/evidence-manifest.md`: available and missing evidence.

## Reproduction
Use an authorized, isolated SOC Lab. Verify sensor health, timestamps, asset ownership, and the time filter before beginning. Apply `docs/triage-procedure.md` to a new, clearly bounded monitoring session. Record each case's triage-start and decision times independently; do not backfill historical durations.

## Security and publication
Before publishing, inspect the full Git diff and evidence image for usernames, secrets, unredacted host details and identifiers. Raw alerts may contain sensitive information and are not included as published evidence here.

## Remaining work for a complete demonstration
A newly measured session with at least two distinct case-level decisions, defensible queue deduplication, and a controlled end-to-end incident-response scenario (or a clearly documented limitation) remain to be validated. Existing documentation does not establish successful technical containment or recovery.

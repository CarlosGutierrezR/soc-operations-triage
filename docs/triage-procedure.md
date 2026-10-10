# SOC triage procedure

1. **Scope the shift** — Record UTC start/end, timezone, monitored assets, SIEM query, filters and data-source health. Never call a retrospective 24-hour search a 24-hour staffed shift.
2. **Queue intake** — Preserve source alert identifiers, event and ingestion timestamps, sensor, rule, severity and raw-event references. A SIEM hit is not a unique incident.
3. **Deduplicate** — Group only when rule, asset, process/parent context and justified time window agree; preserve all underlying event IDs and record the grouping rationale. Do not collapse distinct activity solely because rule IDs match.
4. **Prioritize** — Apply `severity-model.md` using affected asset, plausible impact, confidence, recurrence, and contextual indicators. Rule level alone does not determine incident severity.
5. **Investigate** — Compare process lineage, command line, account, signature, scheduled tasks/service context, adjacent activity and related telemetry when available. Separate *observation*, *inference*, and *unverified hypothesis*.
6. **Decide** — Document benign/likely benign, suspicious, confirmed incident, or inconclusive; state confidence and residual uncertainty. A valid executable signature is insufficient to prove benign intent.
7. **Act and escalate** — Follow `escalation-matrix.md`. No destructive containment without scope, approval, preservation plan and rollback.
8. **Record times** — For new cases, capture first event, first visible alert, triage start, decision and closure/escalation in UTC as separate fields. Calculate triage duration only when both valid human-work timestamps exist.
9. **Handover** — State case ID, current owner/status, what is known, what remains unknown, next action and deadline if one is actually agreed.
10. **Close and learn** — Register evidence IDs, documented decisions, and candidates for rule tuning; require negative tests before suppression.

## Required per-case fields
Case ID, alert IDs, agent, UTC timestamps, rule, initial priority, analyst hypothesis, evidence, observations, limitations, disposition, justification, action, escalation/closure status, handover and tuning candidate.

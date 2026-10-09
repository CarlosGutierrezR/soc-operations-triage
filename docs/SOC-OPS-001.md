# SOC-OPS-001 — Initial SOC Monitoring & Triage

## Problem statement

A SOC analyst starts a monitoring shift with security alerts and findings from heterogeneous telemetry sources.

Not every alert represents a confirmed security incident. The analyst must prioritize, investigate, document and resolve or escalate cases while preserving evidence and operational traceability.

## Objective

Perform a controlled SOC monitoring shift using the existing shared SOC Lab.

Demonstrate evidence-based alert prioritization, triage, investigation, incident determination, escalation, closure and shift handover.

## Scope

- Wazuh endpoint and identity telemetry.
- Security Onion network telemetry through Zeek and Suricata.
- Manual alert triage and case documentation.
- Evidence correlation between available data sources.
- Incident response decisions when justified.
- Metrics derived from observed timestamps.
- Identification of detection improvements and automation opportunities.

## Out of scope — Initial iteration

- Installing a new SIEM or case management platform.
- Reconfiguring shared SOC infrastructure.
- Unapproved offensive activity.
- Automatic containment.
- Claiming simulated incidents represent production incidents.

## Operational workflow

Telemetry → Detection → Alert → Monitoring → Triage → Investigation → Determination → Response → Closure → Metrics → Automation opportunities.

## Validation criteria

- Required telemetry sources are audited before the shift.
- Alert records have traceable source identifiers and timestamps.
- Each investigated case includes hypothesis, evidence, analysis and determination.
- Escalation and closure decisions are documented.
- A shift handover identifies outstanding work.
- Metrics are calculated from observed data.
- Limitations and gaps are explicitly recorded.

## Current status

**Planning.** Repository initialized. Telemetry health, shift execution and operational results have not yet been validated.

## Security constraints

All testing remains within the authorized SOC Lab. Shared infrastructure changes require separate approval and validation. Evidence must be sanitized before public publication.
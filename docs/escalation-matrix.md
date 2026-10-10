# Escalation and disposition matrix

| Analyst disposition | Evidence threshold | Action |
|---|---|---|
| Confirmed incident | Corroborated unauthorized activity or controlled scenario with verified ground truth | Escalate and document incident timeline, scope, proposed containment, approval, recovery and lessons learned |
| Suspicious / unresolved high impact | Plausible harmful behavior with missing decisive evidence | Escalate for additional collection; preserve artifacts and explicit owner |
| Inconclusive | Insufficient confirmation or rebuttal | Keep investigation open or hand over with a precise missing-evidence checklist |
| Likely benign, residual uncertainty accepted | Multiple benign contextual indicators, no compromise substantiated, analyst accepts documented limitations | Administrative closure without falsely claiming verified harmlessness or a confirmed false positive |
| Confirmed benign | Sufficient provenance and corroboration | Close with source-linked rationale |

**Response guardrails:** no isolation, service stop, account disablement, firewall changes, deletion or production changes without explicit approval, blast-radius check, backups/rollback and observed validation.

**CASE-001 decision:** The analyst explicitly authorized administrative closure on 2026-10-10 as *Likely Benign — Closed with Residual Uncertainty*, no containment. This is not proof of the Wazuh SCA parent chain.

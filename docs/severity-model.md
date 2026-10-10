# SOC priority model

**Priority is not identical to Wazuh rule level.** Start with source level, then evaluate asset criticality, credible impact, exposure, behavioral context, recurrence, corroborating signals and uncertainty.

| Priority | Trigger examples | Expected treatment |
|---|---|---|
| Critical | Credible active compromise with urgent material impact | Immediate escalation; preserve evidence; containment only on authorization |
| High | High-impact behavior or credible suspicious technique requiring prompt context review | Prioritized investigation and handover if unresolved |
| Medium | Suspicious or ambiguous activity with limited corroboration | Routine investigation and context enrichment |
| Low | Contextually expected or low-impact signal without suspicious corroboration | Document rationale; batch only with valid dedup criteria |

For `92058`, **High** was the observed initial queue priority, not a confirmed incident severity. For `92066`, historical case priority was not recorded; do not fabricate a retrospective value.

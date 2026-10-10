# Evidence and measurement limitations

- The existing alert hit counts refer to moving 24-hour windows, not distinct incidents or completed monitoring shifts.
- `SOC-OPS-003`'s 120.34 minutes are wall-clock elapsed time between recorded timestamps, not effective analysis time.
- Individual triage durations and detection/response-time metrics were not reliably captured; leave them null.
- `CASE-001`: SCA proximity does not prove process ancestry; Wazuh query returned no confirming parent event. Filesystem-redirection discrepancy and executable provenance remain unresolved.
- `CASE-002` / Wazuh rule `92058`: Authenticode `Valid` does not establish benign operation; originating compatibility task is not independently identified. Source alert time ordering warrants independent clock/ingestion review.
- A Wazuh alert mapped to ATT&CK indicates detection metadata, not a verified adversarial technique.
- No validated end-to-end incident response, technical containment or recovery is included at this checkpoint.
- No direct network telemetry evidence is yet incorporated into this repository, despite the documented SOC Lab capability.
- Source exports for the investigated alerts have not been sanitized for public inclusion.

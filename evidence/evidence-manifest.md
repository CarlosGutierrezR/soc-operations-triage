# Evidence manifest — Project 4

| Evidence ID | Case | File | What it proves | Publication note |
| --- | --- | --- | --- | --- |
| P4-E002 | CASE-001 | `cases/CASE-001/P4-E002-wazuh-sca-events-sanitized.png` | Wazuh SCA events were visible for agent 001 around the date/time under investigation; supports temporal correlation, not definitive parent-process attribution | Cropped to the Wazuh results area; review before public push |

## Provenance and limitations
- Source: user-provided screenshot of Wazuh Configuration Assessment / Events, 2026-10-09.
- Sanitization: browser/VMware chrome and user-session interface elements were removed by cropping; the analytic table remains as originally captured.
- The displayed query covers multiple days; `20 hits` is **not** a count of incidents or a shift metric.
- The evidence does not prove SCA launched `powershell.exe`.
- Raw incident data and original unredacted screenshots remain outside this proposed public commit.

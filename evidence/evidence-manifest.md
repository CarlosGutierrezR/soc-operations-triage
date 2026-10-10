# Manifiesto de evidencias | Proyecto 4

## Criterio de trazabilidad

Una referencia a un ID Wazuh **no equivale** a tener su JSON original versionado. Se distingue entre evidencia incorporada al repositorio, datos estructurados de operación y eventos consultados durante el análisis que **no están incluidos** en este paquete.

| Ref. | Investigación | Evidencia | Disponible en el paquete | Alcance |
|---|---|---|---|---|
| P4-E002 | CASE-001 | `evidence/cases/CASE-001/P4-E002-wazuh-sca-events-sanitized.png` | **No incluida en el ZIP recibido**; la ruta estaba versionada anteriormente en GitHub | Correlación temporal aproximada con SCA, no ascendencia confirmada |
| P4-C001 | CASE-001 | Alerta `1791560105.194937`, Sysmon / regla 92066 | JSON no incluido | Identidad de alerta y contexto PowerShell/SecEdit |
| P4-C002 | CASE-002 | Registro de evento `11:46:53.224 UTC`, regla 92058 | JSON no incluido | Hipótesis de compatibilidad, aún abierta |
| P4-T001 | TRIAGE-001 | Alerta `1791640013.366353`, regla 92058 | JSON original no incluido; métricas en `shifts/SOC-OPS-004-triage.jsonl` | Decisión y duración transcurrida |
| P4-T002 | TRIAGE-002 | Alerta `1791637724.356447`, regla 61102, EID 1129 | JSON original no incluido; métricas en JSONL | Conectividad AD fallida y handover |
| P4-D001 | Deduplicación | Alertas `1791636412.350932` y `1791640013.366353` | JSON originales no incluidos | Dos ejecuciones distintas, sin duplicados entre ellas |
| P4-IR-A | IR-001 | Wazuh `1791644001.430931`, regla 554 | JSON original no incluido | Archivo de prueba añadido (34 bytes) |
| P4-IR-M | IR-001 | Wazuh `1791644001.431630`, regla 550 | JSON original no incluido | Modificación de 34 a 77 bytes y diff |
| P4-IR-R | IR-001 | Wazuh `1791645056.445431`, regla 550 | JSON original no incluido | Restauración a 34 bytes y hash inicial |
| P4-OPS-004 | SOC-OPS-004 | `shifts/SOC-OPS-004-session.json`, `shifts/SOC-OPS-004-triage.jsonl`, `metrics/SOC-OPS-004-summary.csv` | Sí | Fechas, estados y duraciones registradas |

## Qué debe revisar quien publique

1. Confirmar si la imagen P4-E002 del repositorio GitHub vigente sigue disponible, funciona su enlace y está correctamente sanitizada.
2. No subir JSON originales ni capturas con usuarios, credenciales, tokens, rutas locales personales o datos sensibles sin revisión específica.
3. Conservar originales y hashes fuera del repositorio público si se necesitan para una cadena de custodia más estricta.
4. No presentar los tres eventos de IR-001 como capturas disponibles en GitHub: fueron proporcionados para el análisis, pero **no se empaquetaron como ficheros de evidencia**.

La recuperación de IR-001 puede seguirse técnicamente en [el caso](../cases/IR-001.md) mediante alert IDs, SHA256, tamaños y diff, aunque falta una exportación sanitizada de los documentos fuente para reproducción íntegra por terceros.

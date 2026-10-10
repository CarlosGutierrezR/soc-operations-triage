# CASE-001 | Ejecución de SecEdit durante una evaluación de seguridad

## 1. Estado del caso

**Cerrado administrativamente el 10 de octubre de 2026**, por decisión expresa del analista, como **probablemente benigno con incertidumbre residual**. No se confirmó un falso positivo ni un incidente malicioso. No se ejecutaron medidas de contención y **no se registró la hora exacta de cierre**.

## 2. Objetivo de la investigación

Determinar si una exportación de directivas de seguridad mediante `SecEdit.exe` iniciada desde PowerShell estaba relacionada con una comprobación SCA del agente Wazuh o requería escalado.

## 3. Alerta y contexto inicial

| Campo | Valor observado |
|---|---|
| Agente | `WIN11-EP-01` (`001`) |
| Fuente | Wazuh / Windows Sysmon Event ID 1 |
| Regla | `92066`, nivel 4 |
| Wazuh Alert ID | `1791560105.194937` |
| `_id` | `IHRNIaEBANGddl5nx_JB` |
| Evento UTC | `2026-10-09T15:35:04.166Z` |
| Alerta UTC | `2026-10-09T15:35:05.309Z` |
| Cuenta | `NT AUTHORITY\SYSTEM` |
| Proceso | `C:\Windows\SysWOW64\SecEdit.exe` |
| Padre | `C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe` |
| Directorio de trabajo | `C:\Program Files (x86)\ossec-agent\` |
| GUID padre | `{181cb712-09a7-6ac9-e800-000000001800}` |
| GUID hijo | `{181cb712-09a8-6ac9-ea00-000000001800}` |

## 4. Procedimiento documentado

**Paso 1 — Revisar el evento Sysmon.** La alerta de proceso muestra `SecEdit.exe /export /cfg ...\secpol.cfg`. El comando del padre exporta la directiva local, busca el parámetro `ResetLockoutCount` y elimina el archivo temporal. Es una operación compatible con una comprobación de configuración, pero puede necesitar contexto.

**Paso 2 — Revisar la cuenta y el directorio de ejecución.** La cuenta es `SYSTEM` y el directorio de trabajo coincide con la instalación del agente. Es una pista contextual, no identificación concluyente del origen.

**Paso 3 — Correlacionar con Wazuh SCA.** Se observó en el dashboard actividad SCA próxima temporalmente para el agente `001`, en torno a las 17:35–17:44 de la hora local mostrada. La imagen sanitizada [P4-E002](../evidence/cases/CASE-001/P4-E002-wazuh-sca-events-sanitized.png) conserva esa observación. La conversión horaria formal de la captura no se validó.

**Paso 4 — Intentar confirmar el árbol de procesos.** La búsqueda por `parentProcessGuid` no devolvió un proceso padre concluyente en el índice consultado. **Una búsqueda sin resultados no demuestra que el proceso no existiera.**

**Paso 5 — Evaluar discrepancias.** Los campos de imagen y comando reflejan rutas Windows `SysWOW64` y `system32` no reconciliadas. No se comprobaron independientemente firma ni hash del ejecutable.

## 5. Análisis y decisión

**Observado:** ejecución bajo SYSTEM, exportación de política local, directorio del agente y eventos SCA cercanos.

**Hipótesis:** actividad iniciada por Wazuh SCA. **No confirmada**, porque no se recuperó la línea de ascendencia completa del proceso padre.

La regla etiqueta `T1059.001` (PowerShell), lo que describe la detección; no demuestra uso malicioso. El 10/10/2026 se autorizó el cierre administrativo **con incertidumbre residual explícitamente aceptada**. La razón fue la compatibilidad contextual con una revisión de configuración, no una prueba definitiva de procedencia benigna.

## 6. Estado final y reapertura

- Clasificación: probablemente benigno, no confirmado.
- Contención/remediación: ninguna.
- Prioridad histórica: no documentada.
- Inicio/fin de triage y duración: no disponibles; no reconstruirlos.
- Reabrir si aparece evidencia contradictoria o ascendencia del proceso fiable.

**Evidencias:** captura [P4-E002](../evidence/cases/CASE-001/P4-E002-wazuh-sca-events-sanitized.png) y JSON original de alerta suministrado en el análisis, **no incluido en Git público**. Véase el [manifiesto](../evidence/evidence-manifest.md).

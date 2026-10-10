# SOC-OPS-003 | Priorización y primer análisis de `sdbinst.exe`

## 1. Sesión registrada

| Campo | Valor |
|---|---|
| Fecha | 2026-10-10 |
| Herramienta | Wazuh Threat Hunting |
| Tipo | Sesión interrumpida de monitorización y triage |
| Inicio UTC | `2026-10-10T10:50:50.7664302Z` |
| Fin UTC | `2026-10-10T12:51:11.2721167Z` |
| Tiempo transcurrido | **120,34 minutos** |
| Trabajo efectivo | No medido |

La diferencia inicio–fin **no** representa 120,34 minutos de análisis continuo.

## 2. Paso 1 — Revisar la cola

Filtro: manager `soc-wazuh-01`, últimas 24 horas; la ventana visible abarcaba aproximadamente 2026-10-09 14:44 a 2026-10-10 14:44. Se observaron **192 hits**. No se calculó el número de incidentes distintos.

| Regla | Nivel | Señal visible | Prioridad inicial |
|---|---:|---|---|
| `92058` | 12 | Base de compatibilidad iniciada | Alta |
| `61102` | 5 | Error del sistema Windows | Media |
| `92052` | 4 | Consola de comandos iniciada por proceso inusual | Media |
| `61104` | 3 | Cambio de tipo de inicio de servicio | Media-baja |
| `60608` | 4 | Evento resumido de firmas | Baja |

Son **familias presentes en la captura revisada**, no un desglose exhaustivo de los 192 hits.

## 3. Paso 2 — Investigar la regla 92058

En `WIN11-EP-01`, Sysmon Event ID 1 registró a las `2026-10-10 11:46:53.224 UTC` el proceso `sdbinst.exe -m -bg`, padre `svchost.exe` (`PcaSvc`) bajo `SYSTEM`. La comprobación Authenticode devolvió `Valid`; el sujeto del certificado no quedó registrado.

**Interpretación:** el contexto se asemeja a una operación de compatibilidad de Windows; no demuestra su procedencia legítima. La secuencia de marcas horarias entre alerta y evento resultó inconsistente. El mapeo `T1546.011` es metadato de detección, no indicio concluyente de persistencia.

## 4. Paso 3 — Determinar y transferir

- Investigación detallada documentada: **1**.
- Clasificación: probablemente legítimo, **sin confirmar**.
- Estado: abierto en [CASE-002](../cases/CASE-002.md).
- Contención: ninguna.
- Tiempo individual de triage: no registrado.
- Confirmación de incidentes maliciosos: no establecida.

## 5. Cierre de la sesión

Se transfirió la comprobación de procedencia de `sdbinst.exe` y la revisión de errores Windows `61102`. La fase posterior [SOC-OPS-004](SOC-OPS-004.md) sí registró tiempos de dos triages, pero no sustituye las mediciones ausentes de esta sesión.

**Evidencia de tiempo:** [inicio](SOC-OPS-003-start.txt), [fin](SOC-OPS-003-end.txt).

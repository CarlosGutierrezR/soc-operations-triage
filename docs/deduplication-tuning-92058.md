# Regla 92058 | Recurrencia, deduplicación y evaluación de tuning

## 1. Pregunta de análisis

Durante el triage de `WIN11-EP-01` aparecieron ejecuciones de `sdbinst.exe -m -bg` bajo `SYSTEM`, con `svchost.exe` / `PcaSvc` como contexto padre. Antes de agrupar las alertas había que comprobar si correspondían al mismo evento repetido o a procesos distintos.

**Alcance:** únicamente dos JSON de Wazuh del 10 de octubre de 2026. No se extrajo ni evaluó la cola completa.

## 2. Procedimiento seguido

1. Filtrar en Wazuh Threat Hunting por `rule.id: 92058` y el agente Windows.
2. Abrir los documentos originales y comparar `id` de Wazuh, `_id`, `eventRecordID`, `processGuid`, `processId` y `utcTime` de Sysmon.
3. Revisar el comando, hash SHA256, usuario y proceso padre para establecer semejanzas de comportamiento.
4. Determinar si se trata de duplicación **del mismo evento fuente** o de recurrencia de una actividad.
5. Evaluar la conveniencia de cambiar la regla únicamente con lo observado.

## 3. Evidencias comparadas

| Campo | Ejecución A | Ejecución B |
|---|---|---|
| Wazuh Alert ID | `1791636412.350932` | `1791640013.366353` |
| `_id` del documento | `kIfaJaEB5s0dU_04RLJQ` | `vIcRJqEB5s0dU_04M7Ln` |
| `eventRecordID` | `52224` | `53051` |
| `processGuid` | `{181cb712-33bd-6aca-2b02-000000001900}` | `{181cb712-41ce-6aca-4802-000000001900}` |
| Sysmon `utcTime` | `2026-10-10 12:46:53.779` | `2026-10-10 13:46:54.178` |
| PID | `4924` | `3220` |

Coincidencias: ruta `C:\Windows\System32\sdbinst.exe`, comando `sdbinst.exe -m -bg`, usuario `NT AUTHORITY\SYSTEM`, padre `PcaSvc` y SHA256 `8F67CBBDB8250CEDA1E5DB21DF87AD870576229B8FD729E80F9092EB578B6915`. Ambos registros comparten `parentProcessGuid`.

**Resultado observable:** los Process GUID, PID, IDs de registro y alert IDs son distintos. Las ejecuciones están separadas por **1 h y 0,399 s** según `utcTime`.

## 4. Determinación

- Documentos distintos examinados: **2**.
- Ejecuciones Sysmon distintas: **2**.
- Duplicados de un mismo evento en esta comparación: **0**.
- Actividad recurrente bajo un mismo contexto: **sí, en la muestra**.
- Duplicados de toda la cola: **no medidos**.

La similitud de comandos **no autoriza** a eliminar ninguno de los eventos. Podrían vincularse como contexto de una investigación, manteniendo ambas identidades.

## 5. Decisión sobre tuning

**No modificar la regla 92058.** La actividad es compatible con funciones legítimas de compatibilidad de aplicaciones, pero no se verificó la operación que la provocó. El mapeo ATT&CK `T1546.011` pertenece a la regla, no prueba persistencia maliciosa.

No se realizaron pruebas positivas/negativas de una regla alternativa ni se midió tasa de falsos positivos. Una exclusión de `sdbinst.exe` o de `PcaSvc` carecería de soporte suficiente y podría ocultar actividad relevante.

## 6. Evidencia y limitaciones

La comparación se hizo a partir de los JSON compartidos durante la investigación. Estos JSON **no están incorporados como ficheros al paquete público**. Conservar las referencias de origen y documentar esa limitación evita atribuir al repositorio una evidencia que no contiene.

Relacionado: [CASE-002](../cases/CASE-002.md), [SOC-OPS-004](../shifts/SOC-OPS-004.md), [manifiesto](../evidence/evidence-manifest.md).

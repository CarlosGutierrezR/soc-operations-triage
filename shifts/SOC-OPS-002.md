# SOC-OPS-002 | Primera revisión retrospectiva de alertas

## Objetivo

Revisar una muestra de actividad Wazuh y practicar una determinación inicial sin interpretar el recuento de alertas como incidentes.

## Paso 1 — Delimitar la observación

- Plataforma: Wazuh.
- Consulta: **últimas 24 horas**, revisión retrospectiva del 8 al 9 de octubre de 2026.
- Filtro de manager: `soc-wazuh-01`.
- Resultado mostrado: **101 hits**.
- Incidentes distintos y alertas completamente investigadas: **no determinados**.
- No fue un turno atendido durante 24 horas.

## Paso 2 — Analizar una regla representativa

**Regla Wazuh `92052`**, Sysmon Event ID 1, `WIN11-EP-01`:

| Campo | Observación |
|---|---|
| Hora de evento UTC | `2026-10-09 15:45:59.182` |
| Proceso | `C:\Windows\System32\cmd.exe` |
| Padre | `svchost.exe`, servicio `Schedule` |
| Cuenta | `NT AUTHORITY\SYSTEM` |
| Script | `C:\Windows\System32\hpatchmonTask.cmd` |
| ATT&CK informado por la regla | `T1059.003` |

## Paso 3 — Determinar y registrar límites

El contexto sugiere actividad de mantenimiento programado, pero **no se verificaron la tarea concreta ni el origen del script**. El dictamen quedó como probablemente mantenimiento, **pendiente de validación**. No se realizó contención.

## Resultado

La sesión dejó una primera hipótesis y mostró la necesidad de registrar identificadores de origen y tiempos individuales. No se calculó duración del triage, falsos positivos, MTTA ni MTTR. La cifra de 101 hits no debe sumarse con los 192 de la sesión siguiente, que utiliza otra ventana móvil.

**Continuación:** [SOC-OPS-003](SOC-OPS-003.md) y [handover inicial](handover-001.md).

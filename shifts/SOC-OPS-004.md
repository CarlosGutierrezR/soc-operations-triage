# SOC-OPS-004 | Triage cronometrado y transferencia operativa

## 1. Objetivo y alcance

Documentar dos investigaciones retrospectivas de Wazuh con un inicio y un fin de triage registrados en cada una. **No** se trató de monitorización continua de 24 horas ni de una evaluación de toda la cola.

| Registro | UTC |
|---|---|
| Inicio de sesión | `2026-10-10T13:51:00.4501922Z` |
| Fin de sesión | `2026-10-10T14:17:05.2072724Z` |
| Tiempo total transcurrido | **1564,76 s (26 min 4,76 s)** |
| Tiempo efectivo del analista | **No medido** |

Fuentes reproducibles: [JSON de sesión](SOC-OPS-004-session.json), [JSONL de triages](SOC-OPS-004-triage.jsonl), [CSV resumen](../metrics/SOC-OPS-004-summary.csv).

## 2. Triage 001 — Regla 92058

**Pregunta:** ¿la ejecución de `sdbinst.exe` prueba actividad maliciosa?

1. Se seleccionó la alerta `1791640013.366353` de `WIN11-EP-01` (agente `001`), nivel 12, Sysmon Event ID 1.
2. Se revisaron `sdbinst.exe -m -bg`, cuenta `SYSTEM` y el servicio padre `PcaSvc`.
3. Se identificó un contexto compatible con funciones de compatibilidad de Windows, sin operación origen acreditada.
4. Se mantuvo el dictamen **probablemente benigno, sin confirmar** y el seguimiento pendiente.

**Medición registrada:** `14:03:21.1424749Z` → `14:05:25.7584189Z` = **124,62 s transcurridos**. La alerta precede la hora Sysmon del mismo evento unos 819 ms según sus campos; no se estima latencia de detección.

## 3. Triage 002 — Regla 61102

**Pregunta:** ¿el error de Group Policy refleja un ataque o un fallo operativo?

1. Se revisó la alerta `1791637724.356447` de `WIN11-EP-01`, con **Windows GroupPolicy Event ID 1129** y error `1222` (red no disponible o no iniciada).
2. Desde el propio endpoint se comprobó resolución `DC01.soclab.test` y SRV del dominio: **timeout**.
3. `nltest /dsgetdc:soclab.test` devolvió **1355**. Las pruebas TCP hacia el DC en los puertos **389 y 445** fallaron.
4. `Test-ComputerSecureChannel` devolvió `False` durante la falta de comunicación. Esto **no confirma** que la relación de confianza del equipo esté dañada.
5. `gpresult /r` mostró información de una aplicación previa de la directiva. En el log coexistían eventos 1129 y 1500, por lo que no se dedujo conectividad actual a partir del evento de éxito.
6. Se determinó **fallo operativo de conectividad con AD; causa raíz sin verificar**, y se transfirió a SOC CORE. No hubo contención.

**Medición registrada:** `14:08:19.1731710Z` → `14:17:05.2072724Z` = **526,03 s transcurridos**.

## 4. Resultados y métricas

| Indicador | Valor respaldado |
|---|---:|
| Triages documentados | 2 |
| Triage 001 | 124,62 s |
| Triage 002 | 526,03 s |
| Media/mediana | 325,32 s |
| Trabajo efectivo, MTTR, MTTD | No medidos |
| Incidentes de seguridad confirmados | Ninguno establecido por estos dos triages |
| Deduplicación de toda la cola | No evaluada |

Se mide tiempo desde el comienzo hasta la decisión, **incluidas esperas**. La cifra no representa tiempo neto de trabajo.

## 5. Transferencia y límites

[Handover de la sesión](handover-002.md): procedencia de `sdbinst.exe` pendiente y revisión del DC delegada en SOC CORE. Se preserva la independencia de CASE-002 histórico y de las ejecuciones evaluadas más tarde en [regla 92058](../docs/deduplication-tuning-92058.md).

No se cambió la infraestructura compartida. Los JSON completos de Wazuh no se publicaron; el repositorio conserva sus IDs de referencia.

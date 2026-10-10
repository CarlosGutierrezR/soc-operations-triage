# Operaciones SOC | Monitorización, triage y respuesta a incidentes

> **Proyecto práctico de portfolio.** Trabajo realizado en un laboratorio SOC propio y autorizado. Los casos reflejan observaciones y decisiones documentadas; no representan actividad en un SOC empresarial ni ataques reales confirmados.

## 1. ¿Qué se quiso resolver?

El objetivo fue recorrer el trabajo cotidiano de un analista SOC: recibir alertas, decidir cuáles requieren atención, investigar procesos y registros, diferenciar un hallazgo técnico de un incidente confirmado, transferir lo que no puede cerrarse y verificar una recuperación.

El proyecto reutiliza el **único SOC Lab compartido**. No se desplegó otra infraestructura ni se alteraron reglas compartidas para obtener resultados. La telemetría del endpoint Windows procede de Sysmon y Wazuh; la práctica de recuperación utiliza Wazuh FIM en Linux. **No se presenta correlación Zeek/Suricata–endpoint como resultado demostrado.**

## 2. Recorrido de lectura recomendado

| Orden | Documento | Qué permite comprobar |
|---|---|---|
| 1 | [Procedimiento de triage](docs/triage-procedure.md) | Método, criterios de registro y decisiones |
| 2 | [Modelo de prioridades](docs/severity-model.md) y [escalado](docs/escalation-matrix.md) | Cómo se decide prioridad y respuesta |
| 3 | [SOC-OPS-002](shifts/SOC-OPS-002.md) | Primera revisión retrospectiva: 101 hits |
| 4 | [SOC-OPS-003](shifts/SOC-OPS-003.md) | Cola inicial, 192 hits y análisis de `sdbinst.exe` |
| 5 | [CASE-001](cases/CASE-001.md) y [CASE-002](cases/CASE-002.md) | Cierre administrativo y caso abierto, respectivamente |
| 6 | [SOC-OPS-004](shifts/SOC-OPS-004.md) | Dos triages cronometrados y decisión de escalado |
| 7 | [Comparación de alertas 92058](docs/deduplication-tuning-92058.md) | Recurrencia frente a duplicación; decisión de no suprimir |
| 8 | [IR-001](cases/IR-001.md) | Preparación, modificación controlada, tres alertas FIM y restauración |
| 9 | [Lecciones aprendidas](docs/IR-001-lessons-learned.md), [limitaciones](docs/limitations.md) y [evidencias](evidence/evidence-manifest.md) | Qué quedó demostrado y qué no |

El [planteamiento inicial](docs/SOC-OPS-001.md) se conserva como documento histórico: sus referencias a «planificación» **no describen el estado final**.

## 3. Entorno utilizado y verificado durante el trabajo

| Función | Componente | Evidencia de uso |
|---|---|---|
| Estación del analista | `SOC-Analyst-WS` | Acceso y consultas, incluido SSH al endpoint Linux |
| Endpoint Windows | `WIN11-EP-01`, agente Wazuh `001` | Sysmon Event ID 1 y GroupPolicy Event ID 1129 |
| Endpoint Linux | `LINUX-EP-01`, agente `002`, Ubuntu 24.04.5 LTS | SSH, Wazuh Agent `4.14.7` y FIM en tiempo real |
| SIEM/HIDS | Wazuh Manager `soc-wazuh-01` | Alertas reales con ID de origen conservado |
| Segmento Linux | IP observada `10.50.20.21` | Prueba TCP/22 y sesión SSH desde `10.50.10.100` |

Las direcciones corresponden al laboratorio observado; no son requisitos genéricos de instalación. El inventario puede cambiar, por lo que cada reproducción debe verificar direcciones y alcance.

## 4. Resultados comprobados

| Actividad | Evidencia | Resultado |
|---|---|---|
| CASE-001 | Regla `92066`, Sysmon y contexto SCA | Cerrado administrativamente como probablemente benigno, con incertidumbre residual aceptada |
| CASE-002 | Regla `92058` y firma de `sdbinst.exe` | Permanece abierto; procedencia exacta no comprobada |
| SOC-OPS-002 | Filtro relativo 24 h | 101 coincidencias, no 101 incidentes |
| SOC-OPS-003 | Otro filtro relativo 24 h | 192 coincidencias, no acumulables a las anteriores |
| SOC-OPS-004 | Dos registros con inicio/fin | 124,62 s y 526,03 s transcurridos; media y mediana 325,32 s |
| Comparación 92058 | Dos alertas distintas y distintos Process GUID | Dos ejecuciones, **cero duplicados entre esos dos eventos**; cola completa sin medir |
| IR-001 | Reglas `554`, `550`, `550` | Creación, modificación y restauración detectadas; SHA256 original recuperado |

En IR-001 se simuló una modificación autorizada de un **archivo de prueba**, no una intrusión real. No se practicó aislamiento de un adversario ni erradicación de malware. La diferencia entre relojes de endpoint y SIEM impide declarar una latencia de detección o un MTTR fiable.

## 5. Flujo de trabajo aplicado

**Telemetría → alerta → priorización → investigación → determinación → escalado o recuperación → validación → documentación.**

Se conservaron los ID de alertas y las limitaciones. Los datos ausentes se dejaron vacíos; no se asignaron tiempos a posteriori. Los 101 y 192 hits provienen de ventanas móviles diferentes y **no se suman**.

## 6. Reproducción y seguridad

1. Usar únicamente un entorno propio, aislado y autorizado.
2. Comprobar agente, conectividad, configuración y hora antes de interpretar alertas.
3. Seguir el [procedimiento de triage](docs/triage-procedure.md) y registrar datos observados, no estimados.
4. Para una prueba FIM, usar exclusivamente un directorio de ensayo previamente autorizado, con baseline y reversión definidos. [IR-001](cases/IR-001.md) recoge el procedimiento realmente ejecutado, **no una instrucción para modificar archivos de producción**.
5. Verificar los resultados en endpoint y SIEM antes de cerrar el caso.

Las capturas y los eventos originales pueden contener información sensible. El [manifiesto](evidence/evidence-manifest.md) separa la evidencia publicada de los JSON facilitados durante la investigación que **no se incorporaron al repositorio**. Revisar siempre imágenes, rutas, usuarios, IP, tokens y diffs antes de publicar.

## 7. Estado y trabajo pendiente

**Alcance demostrado:** investigación de alertas, clasificación, handover, tiempos transcurridos de dos triages, comparación limitada de recurrencia y recuperación FIM controlada.

**Abierto o no demostrado:** procedencia del CASE-002 y de TRIAGE-001; causa raíz del fallo de Active Directory de TRIAGE-002 (transferido a SOC CORE); deduplicación de toda la cola; medición de trabajo efectivo, MTTA/MTTD/MTTR y tasa de falsos positivos; correlación directa red–endpoint; contención de una amenaza real. Véase [limitaciones](docs/limitations.md).

## 🌐 English summary

**SOC operations practice** in my own authorized SOC lab (Wazuh, Sysmon, Windows 11 and Ubuntu endpoints): alert triage, case handling, shift handover and a controlled recovery exercise.

- **Cases:** CASE-001 administratively closed as likely benign with accepted residual uncertainty; CASE-002 still open (exact provenance of `sdbinst.exe` not verified).
- **Shifts:** two retrospective 24 h queue reviews (101 and 192 hits from different rolling windows, not added together) and two timed triages (124.62 s and 526.03 s elapsed).
- **Tuning:** comparison of recurring rule `92058` alerts — two distinct executions, no duplicates between those two events; the full queue was not measured.
- **IR-001:** authorized modification of a test file detected by Wazuh FIM (rules `554`, `550`) and restored to its original SHA-256. It was not a real intrusion.
- **Not demonstrated:** MTTA/MTTD/MTTR, false-positive rate, network–endpoint correlation, or containment of a real threat. See [limitations](docs/limitations.md).

## Licencia

[MIT](LICENSE)

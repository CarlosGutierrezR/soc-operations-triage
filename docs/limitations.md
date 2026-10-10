# Limitaciones, incertidumbres y pendientes

Este documento refleja el **estado posterior a IR-001**, y no el estado inicial de planificación.

| Área | Límite de la evidencia | Consecuencia |
|---|---|---|
| Ventanas SOC-OPS-002/003 | 101 y 192 hits en ventanas móviles diferentes | No sumar ni interpretar como incidentes únicos |
| Tiempo de SOC-OPS-003 | 120,34 minutos transcurridos entre registros | No es tiempo efectivo de análisis |
| SOC-OPS-004 | Dos triages, 124,62 s y 526,03 s | Muestra reducida; tiempos de reloj, no trabajo efectivo |
| CASE-001 | Contexto SCA próximo, sin árbol de procesos padre confirmado | Cierre con incertidumbre, no falso positivo confirmado |
| CASE-002 / regla 92058 | Firma válida y contexto PcaSvc, pero operación de origen no identificada | Caso abierto, no legitimidad demostrada |
| Deduplicación 92058 | Dos eventos diferentes contrastados | No prueba una tasa de duplicados de toda la cola |
| TRIAGE-002 / AD | DNS, descubrimiento y TCP al DC fallaron al consultar | Causa raíz y reparación pendientes en SOC CORE |
| IR-001 | Archivo ficticio; creación, modificación y restauración verificadas | No constituye ataque real, contención ni erradicación |
| Relojes | Hora de Linux indicada como UTC difiere alrededor de dos horas de la marca SIEM | No calcular latencia de detección ni MTTR |
| Evidencias de origen | Varios JSON facilitados durante la investigación no están en el Git público | Trazabilidad por ID, no reproducción íntegra desde el repositorio |
| Red | No se incorporó correlación concreta Zeek/Suricata–host | No reclamar esa capacidad como resultado de Proyecto 4 |

**Nota sobre Wazuh ATT&CK:** una técnica indicada en la regla representa una correspondencia del detector; no demuestra que exista un adversario.

**Mejora de infraestructura propuesta, no ejecutada:** revisar sincronización horaria y conectividad AD desde SOC CORE bajo su proceso de auditoría, rollback y validación.

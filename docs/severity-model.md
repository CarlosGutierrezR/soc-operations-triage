# Modelo de prioridad para alertas SOC

**Prioridad operativa ≠ nivel de regla Wazuh ≠ gravedad de incidente confirmado.** La decisión depende del activo afectado, impacto plausible, exposición, conducta observada, recurrencia, indicadores adicionales y grado de certeza.

| Prioridad | Criterio de uso | Tratamiento |
|---|---|---|
| Crítica | Compromiso activo creíble con impacto urgente | Escalar de inmediato, preservar pruebas y solicitar aprobación para contención |
| Alta | Comportamiento potencialmente grave que exige contexto rápido | Priorizar investigación y transferir si queda inconclusa |
| Media | Señal ambigua o problema operativo que requiere revisión | Investigar alcance y enriquecer contexto |
| Baja | Actividad aparentemente esperable y de bajo impacto, sin corroboración sospechosa | Justificar decisión y agrupar solo con criterios de deduplicación válidos |

## Ejemplos del laboratorio

- **Regla 92058:** prioridad inicial alta por el contexto de la alerta; no implica que se haya confirmado una intrusión.
- **Regla 61102:** triage de conectividad de políticas de grupo; se verificaron fallos operativos, pero no la causa ni actividad maliciosa.
- **CASE-001 / regla 92066:** no se registró una prioridad histórica formal; no se le asigna una ahora de manera retrospectiva.

Véanse [procedimiento de triage](triage-procedure.md) y [matriz de escalado](escalation-matrix.md).

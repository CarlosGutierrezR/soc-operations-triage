# Procedimiento operativo de triage SOC

## Objetivo

Aplicar un método consistente a una alerta de Wazuh, con una decisión explicable y verificable. Este procedimiento no presupone que el evento sea malicioso.

## Secuencia de trabajo

1. **Delimitar la sesión.** Registrar UTC de inicio y cierre, alcance, sensores, filtros e intervalo de búsqueda. Una consulta retrospectiva de 24 horas no equivale a un turno atendido durante 24 horas.
2. **Registrar la alerta original.** Guardar `agent.id`, `rule.id`, `id` de Wazuh, `_id` del documento si existe, fuente, niveles y tiempos de evento/alerta. Mantener JSON sin sanitizar fuera del Git público.
3. **Separar hits, eventos, casos e incidentes.** La misma regla puede activarse por ejecuciones distintas. Para deduplicar, comparar identificadores de origen (por ejemplo `eventRecordID` y `processGuid`), activo, contexto y tiempo; no fusionar registros solo por `rule.id`.
4. **Asignar prioridad inicial.** Consultar [modelo de prioridades](severity-model.md); nivel Wazuh no equivale automáticamente a gravedad del incidente.
5. **Investigar.** Revisar proceso padre, línea de comandos, usuario, servicio o tarea, firma cuando corresponda, actividad cercana y logs relevantes. Anotar por separado **observación**, **hipótesis** y **dato no confirmado**.
6. **Determinar.** Elegir benigno verificado, probablemente benigno, sospechoso, incidente confirmado o inconcluso; expresar la confianza y la incertidumbre restante.
7. **Actuar o transferir.** Aplicar [matriz de escalado](escalation-matrix.md). Contención técnica solo con alcance, autorización, respaldo y rollback.
8. **Medir de forma honesta.** Capturar inicio y fin del triage cuando ocurren. Distinguir tiempo transcurrido de trabajo efectivo. No estimar retrospectivamente horas faltantes.
9. **Registrar handover.** Indicar responsable/destino, evidencia, preguntas pendientes y próxima comprobación; no inventar SLA ni fecha límite.
10. **Cerrar y aprender.** Documentar motivos, validación posterior, oportunidad de tuning y pruebas faltantes. Nunca suprimir una regla por una sola muestra.

## Datos mínimos por caso

ID del caso, ID de alerta, activo, fuente, regla, timestamp, prioridad, descripción, consulta/procedimiento aplicado, evidencias, clasificación, acción, validación, estado y siguiente paso.

## Aplicaciones documentadas

- [CASE-001](../cases/CASE-001.md): cierre administrativo con incertidumbre.
- [SOC-OPS-004](../shifts/SOC-OPS-004.md): dos triages con tiempo transcurrido registrado.
- [IR-001](../cases/IR-001.md): simulación controlada, detección y restauración verificada.

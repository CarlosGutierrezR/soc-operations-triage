# CASE-002 | Ejecución de la base de compatibilidad de Windows

## 1. Estado

**Abierto: pendiente de verificar la procedencia de la operación.** La actividad parece compatible con funciones normales de Windows, pero no existe evidencia suficiente para cerrar el caso como benigno.

## 2. Pregunta de investigación

¿Por qué se ejecutó `sdbinst.exe -m -bg` y qué tarea concreta lo provocó?

## 3. Evidencias observadas

| Campo | Resultado |
|---|---|
| Fuente | Wazuh regla `92058`, nivel 12; Sysmon Event ID 1 |
| Endpoint | `WIN11-EP-01` |
| Hora de evento registrada en SOC-OPS-003 | `2026-10-10 11:46:53.224 UTC` |
| Ejecutable | `C:\Windows\System32\sdbinst.exe` |
| Comando | `sdbinst.exe -m -bg` |
| Padre | `svchost.exe`, contexto de servicio `PcaSvc` |
| Usuario | `NT AUTHORITY\SYSTEM` |
| Firma Authenticode | `Valid`; sujeto exacto del certificado no registrado |
| ATT&CK en regla | `T1546.011` |
| Prioridad inicial | Alta, **no** gravedad de incidente confirmado |

## 4. Procedimiento y razonamiento

1. Se priorizó la regla `92058` por su nivel y la relación de `sdbinst.exe` con bases de compatibilidad.
2. Se revisaron comando, usuario y contexto padre `PcaSvc` en los datos disponibles.
3. Se comprobó la validez de la firma Authenticode; no se conservó el sujeto del certificado.
4. Se compararon las marcas temporales de alerta y evento, detectando una inversión de orden sin explicación verificada.
5. Se conservó la hipótesis de actividad legítima, **sin atribuirla a una operación concreta**.

## 5. Resultado y siguiente paso

No se determinó compromiso, pero tampoco se acreditó la procedencia. No hubo contención. Verificar, cuando sea viable, eventos relacionados de compatibilidad, ascendencia de proceso, tarea o aplicación origen, firma completa y configuración temporal del SIEM/endpoint.

Este caso procede de [SOC-OPS-003](../shifts/SOC-OPS-003.md). La comparación posterior de dos **otros** eventos de la misma regla está en [deduplicación y tuning](../docs/deduplication-tuning-92058.md); **no deben confundirse los ID de esos eventos con el evento histórico de este caso**.

# Handover 002 | Transferencia tras SOC-OPS-004

**Sesión de origen:** [SOC-OPS-004](SOC-OPS-004.md), 10/10/2026. Son decisiones de triage, no un informe de remediación de infraestructura.

## TRIAGE-001 — Regla 92058

- **Alerta:** `1791640013.366353`.
- **Estado:** probablemente benigno, sin procedencia confirmada.
- **Pendiente:** identificar operación concreta que lanzó `sdbinst.exe` y revisar coherencia temporal.
- **Acciones ejecutadas:** análisis y registro; **sin contención**.

## TRIAGE-002 — Regla 61102

- **Alerta:** `1791637724.356447`; Windows Event ID `1129`.
- **Hallazgo observado:** fallo de DNS del dominio y de conectividad TCP al DC (`389`, `445`), `nltest` 1355 y prueba de canal seguro `False` durante la desconexión.
- **Estado:** fallo operativo de conectividad con AD; **causa raíz no comprobada**.
- **Destino:** SOC CORE, por tratarse de infraestructura compartida.
- **Siguiente validación:** disponibilidad de DC01, interfaces, DNS, rutas, servicios relevantes y alcance del fallo a otros equipos.
- **Límite:** no reparar canal seguro ni reconfigurar pfSense, DNS o AD sin auditoría y rollback autorizados.

## Pendientes generales

No hay compromiso malicioso confirmado en estos triages, ni contención técnica ejecutada. La deduplicación posterior de **dos eventos de la regla 92058** está documentada [aparte](../docs/deduplication-tuning-92058.md); no equivale a una medición de toda la cola.

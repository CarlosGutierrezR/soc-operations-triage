# Matriz de determinación y escalado

| Determinación | Evidencia necesaria | Acción permitida |
|---|---|---|
| Incidente de seguridad confirmado | Actividad no autorizada corroborada por datos suficientes | Escalado; alcance y timeline; respuesta autorizada con validación |
| Sospecha relevante | Conducta potencialmente dañina sin prueba decisiva | Recopilación adicional y transferencia documentada |
| Inconcluso | No se puede confirmar ni descartar con el material disponible | Mantener abierto o transferir con tareas concretas |
| Probablemente benigno, con incertidumbre aceptada | Contexto compatible con normalidad y límites explicitados | Cierre **administrativo**, sin etiquetar como falso positivo confirmado |
| Benigno verificado | Procedencia legítima y evidencias suficientes | Cierre fundamentado y trazable |
| Simulación autorizada | Actividad de prueba conocida, objetivo delimitado y evidencia propia | Recuperar/validar solo el artefacto de ensayo; no presentar como ataque real |

## Salvaguardas

No aislar máquinas, bloquear redes, deshabilitar cuentas, eliminar datos ni reiniciar servicios críticos sin comprobar dependencias, alcance, permisos, respaldo, reversión y autorización. Los cambios en sistemas compartidos se elevan a **SOC CORE**.

## Aplicación real

- [CASE-001](../cases/CASE-001.md): cierre administrativo explícito, sin contención.
- [SOC-OPS-004, TRIAGE-002](../shifts/SOC-OPS-004.md): fallo de conectividad con AD, transferido a SOC CORE.
- [IR-001](../cases/IR-001.md): restauración de archivo ficticio, sin contención de adversario.

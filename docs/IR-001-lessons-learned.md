# IR-001 | Lecciones aprendidas

## Lo que funcionó

1. La estación SOC-Analyst-WS accedió por SSH al endpoint autorizado, sin necesidad de cambiar la red.
2. El agente Wazuh `002` tenía conexión al manager y una política FIM centralizada para `/opt/soclab-fim` con monitorización en tiempo real.
3. Las reglas `554` y `550` registraron creación y modificación, incluidos tamaños, hashes y un diff de contenido.
4. Se definió una condición previa a la reversión: el hash del fichero debía coincidir con el valor modificado observado.
5. La vuelta al SHA256 original se verificó **dos veces**, en Linux y en una tercera alerta Wazuh.

## Qué no quedó demostrado

- Ningún atacante real actuó en el laboratorio durante el ejercicio: se usó un archivo ficticio y actividad autorizada.
- No hubo aislamiento, erradicación de malware ni recuperación de una máquina completa.
- El snapshot anterior a la prueba existía en VMware, pero no se comprobó mediante una restauración.
- La restauración se validó para **contenido**, tamaño y permisos observados; no para todos los metadatos previos.
- La diferencia temporal aproximada de dos horas entre endpoint y SIEM impide medir latencia y MTTR de forma fiable.

## Mejoras priorizadas

| Acción propuesta | Justificación | Ámbito |
|---|---|---|
| Auditar origen horario y sincronización de endpoint y manager | Permitir cronologías comparables y métricas defendibles | SOC CORE; requiere aprobación y rollback |
| Mantener ID de alertas y hashes junto a cada informe | Favorecer correlación y comprobación independiente | Documentación P4 |
| Registrar actividad efectiva por separado del tiempo de reloj | Evitar métricas de eficiencia engañosas | Operación SOC |
| Estudiar un ejercicio de mesa de contención | Practicar autorizaciones y decisiones sin afectar servicios | Futuro trabajo, no ejecutado |
| Valorar el almacenamiento de JSON sanitizados | Facilitar reproducción del análisis sin divulgar datos sensibles | Revisión de publicación |

## Resultado

La práctica demuestra **detección y reversión verificable de una alteración simulada**, con límites claros respecto de una respuesta a un compromiso real. No se efectuaron cambios globales en Wazuh, pfSense ni Active Directory.

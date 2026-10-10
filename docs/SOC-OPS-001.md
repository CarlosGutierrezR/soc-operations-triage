# SOC-OPS-001 | Planteamiento inicial del proyecto

**Tipo de documento:** diseño histórico. Describe las metas definidas antes de las sesiones; **no debe leerse como una evaluación del estado actual**.

## Problema

Al iniciar una sesión de monitorización aparecen alertas heterogéneas. Es necesario distinguir señales, actividades legítimas, problemas operativos e incidentes con fundamento, sin convertir cada coincidencia del SIEM en un incidente.

## Objetivo y alcance previstos

1. Trabajar en el SOC Lab compartido con telemetría de Wazuh.
2. Revisar señales disponibles de endpoints e identidad.
3. Priorizar, investigar, documentar decisiones y realizar transferencias de turno.
4. Medir únicamente tiempos y cantidades respaldados por registros.
5. Evaluar detecciones y posibles mejoras sin cambiar reglas sin pruebas.
6. Incorporar correlación con Security Onion/Zeek/Suricata cuando existan evidencias suficientes.

## Límites acordados

No desplegar un SIEM nuevo, no alterar infraestructura global sin autorización, no ejecutar pruebas ofensivas fuera del laboratorio, no automatizar contenciones destructivas ni presentar simulaciones como ataques reales.

## Criterios de validación

Una investigación conserva identificación de la alerta, fuente, hora observada, hipótesis, evidencia, evaluación, incertidumbre y decisión. Las sesiones se delimitan temporalmente y los casos abiertos se transfieren con acciones concretas.

## Evolución posterior

El resultado de estas metas está descrito en [README](../README.md), [SOC-OPS-004](../shifts/SOC-OPS-004.md) e [IR-001](../cases/IR-001.md). La correlación efectiva de telemetría de red con host no se documentó como logro de este proyecto.

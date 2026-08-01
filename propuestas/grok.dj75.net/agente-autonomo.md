---
description: Diseño del agente autónomo potenciado por Grok que se ejecuta dentro del contenedor grok.dj75.net.
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - agente
  - grok
  - autonomia
  - tools
title: Agente autónomo — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# Visión

El contenedor no es solo un shell remoto. Es un **agente** que:

- Usa Grok (API xAI) como cerebro.
- Dispone de herramientas (bash, filesystem, git, red, HTTP, etc.).
- Puede actuar de forma reactiva (cuando el humano escribe en la terminal) o proactiva (tareas de mantenimiento, monitorización, actualización de OKF).
- Respeta las convenciones del skill `okf` y del monorepo de operaciones.

# Componentes del agente

| Componente            | Descripción                                              |
|-----------------------|----------------------------------------------------------|
| Runtime               | Python 3 + venv                                          |
| Cliente API           | xAI / Grok (modelo configurable, p.ej. grok-4 o superior)|
| Tooling               | bash, read/write files, git, curl, jq, etc.              |
| Memoria / estado      | Ficheros en `/var/lib/grok` + opcional vector store ligero|
| Skills / prompts      | Incluye el skill OKF y prompts específicos del entorno   |
| Políticas de confianza| Niveles 1–3 (solo proponer → commit → ejecutar servicios)|

# Modos de operación

1. **Interactivo (principal)**  
   El usuario se conecta por la terminal web y conversa o da órdenes. El agente responde y ejecuta herramientas en el contexto del CT.

2. **Autónomo / de fondo**  
   Un servicio systemd (`grok-agent.service`) puede:
   - Revisar el monorepo / bundle OKF.
   - Detectar drift.
   - Proponer o aplicar cambios (según nivel de confianza).
   - Actualizar `log.md`.
   - Reportar estado.

3. **Híbrido**  
   El mismo proceso atiende tanto la sesión interactiva como las tareas programadas (cron o timer de systemd).

# Integración con OKF y monorepo

- El agente debe conocer y respetar el skill [okf-author](/skills/okf-author.md).
- Puede clonar o montar el repositorio `grok-okf` y el monorepo de operaciones.
- Sigue las políticas de confianza descritas en [agentes-autonomos.md](/propuestas/mono-repo-servidor/agentes-autonomos.md).

# Variables de entorno mínimas

```bash
XAI_API_KEY=...
GROK_MODEL=grok-4          # o el modelo disponible
GROK_AGENT_HOME=/opt/grok-agent
GROK_DATA=/var/lib/grok
GROK_TRUST_LEVEL=1         # 1=solo proponer, 2=commit, 3=ejecutar
```

# Seguridad del agente

- La API key se guarda en un fichero legible solo por el usuario `agent` (o secrets de systemd).
- El agente no debe tener acceso root completo salvo que se justifique.
- Todas las acciones destructivas requieren confirmación humana en nivel 1 y 2.

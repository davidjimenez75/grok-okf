---
description: Arquitectura lógica y física del contenedor grok.dj75.net (agente autónomo + terminal web).
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - arquitectura
  - lxc
  - grok
  - web-terminal
title: Arquitectura general — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# Vista general

```
Proxmox host (pm98.dj75.net o equivalente)
│
├── CT: ct-grok-01  (Debian 13 unprivileged)
│   ├── Hostname / FQDN: grok.dj75.net
│   ├── Runtime agente Grok (Python + tools)
│   ├── ttyd (puerto interno 7681)
│   ├── OpenSSH (opcional, solo claves)
│   ├── Volúmenes: /opt/grok-agent, /var/lib/grok, /home/agent
│   └── Variables: XAI_API_KEY, GROK_MODEL, etc.
│
└── CT proxy (Caddy/Nginx)
    └── https://grok.dj75.net → reverse_proxy → ct-grok-01:7681
        (+ autenticación básica o avanzada)
```

# Componentes principales

1. **Contenedor LXC Debian 13**  
   Base estable, unprivileged, con recursos limitados pero suficientes para inferencia vía API y herramientas locales.

2. **Agente autónomo**  
   Proceso (o conjunto de procesos) que:
   - Usa la API de xAI/Grok.
   - Tiene acceso a herramientas (bash, filesystem, git, red, etc.).
   - Puede ejecutarse de forma reactiva (cuando el usuario habla) o proactiva (tareas programadas / bucles de mantenimiento).

3. **Interfaz web de terminal**  
   ttyd (recomendado) o wetty.  
   Se lanza con un comando personalizado que inicia:
   - Un REPL de chat con Grok, o
   - Una shell donde el usuario puede invocar `grok` / `agent` y el resto de herramientas.

4. **Proxy inverso**  
   Termina TLS, aplica autenticación y reenvía el tráfico WebSocket/HTTP al puerto de ttyd.

# Flujo de uso típico

1. El usuario abre `https://grok.dj75.net` en el navegador.
2. Se autentica (basic auth, token, o mTLS según la política).
3. ttyd abre una sesión de terminal.
4. La sesión arranca directamente en el entorno Grok (chat o shell potenciada).
5. El usuario conversa o da órdenes; el agente ejecuta herramientas y responde.
6. En paralelo, el agente puede tener un servicio de fondo para tareas autónomas.

# Relación con otras propuestas

- Comparte el host Proxmox y la estrategia de contenedores de [pm98.dj75.net](/propuestas/pm98.dj75.net/).
- Puede consumir y actualizar el conocimiento del [mono-repo-servidor](/propuestas/mono-repo-servidor/) y del propio bundle OKF.
- Complementa la visión de agentes autónomos descrita en [agentes-autonomos.md](/propuestas/mono-repo-servidor/agentes-autonomos.md).

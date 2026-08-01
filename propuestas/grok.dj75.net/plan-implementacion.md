---
description: Plan de implementación paso a paso del contenedor y el agente grok.dj75.net.
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - plan
  - implementacion
title: Plan de implementación — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# Fases

## Fase 0 — Preparación

1. Confirmar que existe plantilla `debian-13-dev` (o crearla).
2. Reservar IP / nombre DNS `grok.dj75.net`.
3. Obtener o generar API key de xAI.
4. Decidir nivel de confianza inicial del agente (recomendado: 1).

## Fase 1 — Contenedor base

1. Crear CT LXC unprivileged a partir de la plantilla.
2. Configurar hostname, red, recursos (CPU/RAM/disco).
3. Actualizar sistema y paquetes base.
4. Crear usuario `agent` y estructura de directorios.
5. Configurar locale y zona horaria.

## Fase 2 — Runtime del agente

1. Instalar Python 3 + venv.
2. Clonar o copiar el código del agente a `/opt/grok-agent`.
3. Configurar variables de entorno y secretos.
4. Probar llamada básica a la API de Grok.
5. Implementar o adaptar el wrapper `grok-shell` / REPL.

## Fase 3 — Interfaz web de terminal

1. Instalar o compilar **ttyd**.
2. Crear unidad systemd `ttyd.service` que lance el comando del agente.
3. Configurar autenticación básica en ttyd o en el proxy.
4. Añadir regla de reverse proxy en el CT proxy para `grok.dj75.net`.
5. Verificar acceso HTTPS + WebSocket desde el navegador.

## Fase 4 — SSH y endurecimiento

1. Configurar OpenSSH (solo claves).
2. Aplicar fail2ban o equivalente si se expone.
3. Activar unattended-upgrades.
4. Revisar permisos de secretos y directorios.

## Fase 5 — Autonomía (opcional)

1. Crear `grok-agent.service` para tareas de fondo.
2. Definir timers o cron para tareas periódicas.
3. Integrar con el monorepo / bundle OKF.
4. Documentar el nivel de confianza y las acciones permitidas.

## Fase 6 — Validación y documentación

1. Probar sesión completa desde el navegador.
2. Verificar que el agente puede ejecutar herramientas básicas.
3. Incluir el CT en el plan de backups.
4. Actualizar este bundle OKF (`log.md`, índices).
5. Crear entrada de inventario de red/servicios.

# Criterios de aceptación

- [ ] `https://grok.dj75.net` muestra una terminal funcional.
- [ ] El usuario puede interactuar con Grok desde esa terminal.
- [ ] El contenedor es unprivileged y tiene recursos limitados.
- [ ] Los secretos no están en texto plano legible por todos.
- [ ] Existe backup automático del CT.
- [ ] La documentación OKF está actualizada.

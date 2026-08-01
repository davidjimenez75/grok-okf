---
description: Medidas de seguridad y estrategia de backups para el contenedor del agente grok.dj75.net.
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - seguridad
  - backups
  - agent
title: Seguridad y backups — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# Seguridad

## Principios

- Contenedor **unprivileged**.
- Mínimo privilegio para el usuario `agent`.
- API key de xAI almacenada de forma segura (fichero 600 o secret de systemd).
- Autenticación obligatoria en la interfaz web.
- SSH solo por clave pública.
- Actualizaciones de seguridad automáticas (`unattended-upgrades`).

## Controles concretos

| Control                    | Implementación                              |
|----------------------------|---------------------------------------------|
| Aislamiento                | LXC unprivileged + cgroups                  |
| Acceso web                 | HTTPS + basic auth / forward-auth           |
| Acceso SSH                 | Solo claves, fail2ban opcional              |
| Secretos                   | `/etc/grok/secrets.env` (root:agent 640)    |
| Logging                    | journald + rotación                         |
| Rate limiting              | En el proxy                                 |
| Timeout de sesión web      | Configurado en ttyd / proxy                 |

## Nivel de confianza del agente

Seguir la escala definida en la propuesta de agentes autónomos:

- **Nivel 1**: solo propone cambios (PRs o diffs).
- **Nivel 2**: puede hacer commits en ramas de trabajo.
- **Nivel 3**: puede ejecutar acciones de sistema (solo en entornos controlados).

# Backups

- Incluir el CT en el plan de backups de Proxmox (vzdump).
- Frecuencia recomendada: diaria o cada 12 h según criticidad.
- Retención: al menos 7–14 días + snapshots ZFS si se usa.
- Datos críticos adicionales:
  - `/opt/grok-agent` (código y configuración)
  - `/var/lib/grok` (estado, historial, caches)
  - Ficheros de secretos (con cuidado de no filtrarlos en backups no cifrados)

# Recuperación

1. Restaurar el CT desde backup Proxmox.
2. Verificar que los volúmenes de datos estén montados.
3. Reiniciar los servicios `ttyd` y `grok-agent`.
4. Validar conectividad a la API de xAI.

# Referencias

- Playbook: [Backup y restauración en Proxmox](/playbooks/backup-proxmox.md)

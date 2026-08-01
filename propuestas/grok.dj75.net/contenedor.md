---
description: Definición del contenedor LXC Debian 13 para el agente grok.dj75.net.
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - lxc
  - debian13
  - contenedor
title: Contenedor Debian 13 — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# Especificación del CT

| Parámetro          | Valor recomendado                          |
|--------------------|--------------------------------------------|
| Nombre             | `ct-grok-01`                               |
| Hostname           | `grok` / FQDN `grok.dj75.net`              |
| Plantilla          | `debian-13-dev` (o plantilla específica)   |
| Privilegio         | **unprivileged**                           |
| vCPU               | 2–4                                        |
| RAM                | 4–8 GB                                     |
| Disco              | 40–80 GB (según volúmenes de trabajo)      |
| Red                | vmbr0 (LAN) + IP estática o DHCP reservado |
| Features           | nesting=1 (si se necesitan contenedores internos) |

# Software base a instalar

```bash
apt update && apt full-upgrade -y
apt install -y \
  curl wget git vim htop sudo ca-certificates locales \
  python3 python3-pip python3-venv \
  openssh-server \
  tmux screen \
  jq tree unzip
```

# Usuario y entorno

- Usuario principal: `agent` (con sudo limitado).
- Directorio de trabajo del agente: `/opt/grok-agent`.
- Datos persistentes: `/var/lib/grok` (historial, estado, caches).
- Home: `/home/agent`.
- Locale: `es_ES.UTF-8`.
- Zona horaria: `Europe/Madrid`.

# Servicios systemd recomendados

- `ttyd.service` → interfaz web de terminal.
- `grok-agent.service` → proceso principal del agente (opcional, si se desea autonomía en segundo plano).
- `sshd.service` → acceso SSH clásico (solo claves, fail2ban recomendado).

# Buenas prácticas

- Mantener el CT unprivileged.
- Montar volúmenes bind o ZFS datasets específicos para datos del agente.
- Actualizar la plantilla base periódicamente y reclonar si es necesario.
- Documentar en el propio CT (fichero `/etc/grok-ct.md`) el propósito y los puertos expuestos.

# Referencias

- [Contenedores](/sistemas/contenedores.md)
- [Debian](/sistemas/debian.md)
- Skill: [container-ops](/skills/container-ops.md)

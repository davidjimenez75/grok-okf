---
description: Plan de implementación por fases del servidor Git git.dj75.net sobre Debian 13 y Q1900M.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - plan
  - implementacion
  - debian13
title: Plan de implementación — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Fase 0 — Preparación (1 hora)

- Decidir la opción de software (ver [opciones.md](opciones.md)).
- Reservar IP fija en el router y crear la entrada DNS `git.dj75.net`.
- Tener a mano las claves SSH públicas de los usuarios que accederán.

# Fase 1 — Instalación base de Debian 13 (1–2 horas)

- Instalar Debian 13 (netinst) en modo mínimo.
- Configurar hostname `git`, red estática o DHCP reservation.
- Actualizar el sistema: `apt update && apt full-upgrade`.
- Instalar `openssh-server`, `git`, `ufw` (o configurar nftables).
- Crear usuario de servicio y deshabilitar login root por contraseña.
- Activar `unattended-upgrades`.

# Fase 2 — Despliegue de la opción elegida

## Si Bare Git + SSH

```bash
adduser --system --group --shell /usr/bin/git-shell git
mkdir -p /var/lib/git/repositories
chown -R git:git /var/lib/git
# Añadir claves a /var/lib/git/.ssh/authorized_keys con command="..." si se desea restringir
```

## Si Gitolite

Seguir la guía oficial de instalación sobre el usuario `git`.

## Si Soft Serve

Descargar el binario desde los releases de Charmbracelet o usar el paquete/container si se prefiere. Configurar el directorio de datos y el puerto SSH.

## Si Forgejo

- Descargar el binario oficial.
- Configurar `app.ini` con SQLite, ruta de datos y recursos limitados.
- Crear servicio systemd.
- (Opcional) Instalar Caddy o nginx como proxy.

# Fase 3 — Pruebas (1 hora)

- Crear un repositorio de prueba.
- Clonar desde otra máquina de la LAN.
- Hacer commit + push + pull.
- Verificar permisos (que un usuario no autorizado no pueda escribir).
- Comprobar consumo de memoria con `free -h` y `ps aux --sort=-%mem`.

# Fase 4 — Hardening y backups

- Ajustar firewall.
- Configurar el job de backup (rsync o snapshot).
- Documentar las claves autorizadas y la ubicación de los datos.
- Realizar una restauración de prueba.

# Fase 5 — Documentación y cierre

- Actualizar este directorio de la propuesta con la opción finalmente elegida y los detalles reales (rutas, puertos, etc.).
- Añadir entrada en el `log.md` del bundle.
- (Opcional) Crear un playbook específico de operaciones diarias.

# Criterios de aceptación

- Se puede clonar y hacer push a un repositorio desde al menos dos máquinas de la LAN.
- El consumo de RAM del servicio en reposo es compatible con los 4 GB totales.
- Existe al menos un backup restaurable de los repositorios.
- La documentación de `propuestas/git.dj75.net/` refleja la realidad desplegada.

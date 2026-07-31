---
description: Skill de agente para tareas habituales de administración de sistemas en Debian (paquetes, servicios, logs, seguridad básica y diagnóstico).
generated:
  at: 2026-07-31T08:15:00Z
  by: human:davidjimenez75
status: stable
tags:
  - skill
  - debian
  - linux
  - sysadmin
  - apt
title: debian-sysadmin
type: Skill
verified:
  at: 2026-07-31T08:15:00Z
  by: human:davidjimenez75
---

# Por qué te lo recomiendo

Debian es la base de casi todo tu entorno (#debian + Proxmox). Un skill de administración general te da un «sysadmin asistente» para las tareas repetitivas y de diagnóstico que no están cubiertas por los skills más específicos de Proxmox o LAMP.

# Capacidades sugeridas

- Actualizar el sistema de forma segura (`apt update && apt full-upgrade`) con reporte de cambios.
- Instalar / eliminar / buscar paquetes con explicación de dependencias.
- Gestionar servicios systemd (status, enable, restart, logs recientes).
- Analizar logs del sistema (`journalctl`) filtrando por unidad, prioridad o periodo.
- Comprobar espacio en disco, inodos y uso de memoria de forma legible.
- Revisar configuración básica de seguridad (usuarios, sudo, fail2ban, actualizaciones automáticas).
- Generar un informe de salud del host (uptime, load, actualizaciones pendientes, servicios fallidos).

# Enfoque de implementación

1. Ejecutar comandos vía SSH o localmente con privilegios mínimos necesarios.
2. Preferir `apt` y `systemctl` / `journalctl` (herramientas nativas).
3. Nunca ejecutar `rm -rf` ni cambios irreversibles sin confirmación explícita.
4. Producir salidas estructuradas (tablas o YAML) para que el agente pueda razonar sobre ellas.
5. Integrarse con los skills de Proxmox y contenedores cuando el host sea un nodo o un LXC.

# Relación con el resto del bundle

- Se apoya en [Debian](/sistemas/debian.md).
- Es la base sobre la que se construyen [proxmox-ops](proxmox-ops.md), [container-ops](container-ops.md) y [lamp-ops](lamp-ops.md).

# Prioridad de implementación

**Media-Alta**. Muy útil como skill de soporte general.

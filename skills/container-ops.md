---
description: Skill de agente para gestionar contenedores de sistema (LXC) y de aplicación (Docker/Podman) de forma unificada y segura.
generated:
  at: 2026-07-31T08:10:00Z
  by: human:davidjimenez75
status: stable
tags:
  - skill
  - contenedores
  - docker
  - podman
  - lxc
  - sysadmin
title: container-ops
type: Skill
verified:
  at: 2026-07-31T08:10:00Z
  by: human:davidjimenez75
---

# Por qué te lo recomiendo

Trabajas habitualmente con **LXC en Proxmox** y es muy probable que uses (o uses) Docker/Podman para aplicaciones. Un skill unificado evita tener que cambiar de mentalidad entre `pct`, `docker` y `podman`.

# Capacidades sugeridas

- Listar contenedores en ejecución (LXC + Docker/Podman) con recursos y estado.
- Crear / arrancar / parar / eliminar contenedores.
- Ejecutar comandos dentro de un contenedor (`pct exec`, `docker exec`, `podman exec`).
- Gestionar volúmenes e imágenes (pull, prune, inspect).
- Generar y aplicar `docker-compose` / `podman-compose` básicos.
- Comprobar salud de servicios dentro del contenedor (puertos, procesos).
- Migrar un servicio de LXC a un contenedor de aplicación (o viceversa) cuando tenga sentido.

# Enfoque de implementación

1. Detectar el runtime disponible (Proxmox LXC, Docker, Podman) y exponer una interfaz común.
2. Preferir **Podman rootless** cuando sea posible por seguridad.
3. Para LXC: reutilizar la lógica del skill [proxmox-ops](proxmox-ops.md).
4. Confirmación humana para operaciones destructivas o que afecten a producción.
5. Logging claro de todas las acciones realizadas por el agente.

# Relación con el resto del bundle

- Se apoya en [Contenedores](/sistemas/contenedores.md).
- Trabaja en tándem con [proxmox-ops](proxmox-ops.md) y [lamp-ops](lamp-ops.md).

# Prioridad de implementación

**Alta**. Complementa perfectamente el skill de Proxmox.

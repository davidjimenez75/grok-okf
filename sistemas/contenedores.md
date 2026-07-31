---
description: Tecnologías de contenedorización: LXC (sistema), Docker y Podman (aplicación). Diferencias, cuándo usar cada una y buenas prácticas.
generated:
  at: 2026-07-31T07:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - contenedores
  - docker
  - podman
  - lxc
  - virtualizacion
title: Contenedores
type: Reference
verified:
  at: 2026-07-31T07:35:00Z
  by: human:davidjimenez75
---

# Definición

Los **contenedores** permiten empaquetar y ejecutar aplicaciones o sistemas operativos de forma aislada y ligera, compartiendo el kernel del host.

Existen dos familias principales:

| Tipo              | Ejemplos          | Nivel de aislamiento      | Uso típico                  |
|-------------------|-------------------|---------------------------|------------------------------|
| Contenedor de sistema | LXC, LXD, systemd-nspawn | Casi una VM completa     | Servidores, Proxmox         |
| Contenedor de aplicación | Docker, Podman, containerd | Proceso + namespaces     | Microservicios, CI/CD, apps |

# LXC (Linux Containers)

- Nativo de Proxmox.
- Comparte el kernel del host → muy eficiente en recursos.
- Ideal para servicios tradicionales (Apache, PHP, MySQL, DNS, etc.).
- Se gestiona con `pct` en Proxmox o `lxc`/`lxd` en Debian.

# Docker

- Estándar de facto para aplicaciones.
- Imágenes + capas + volúmenes + redes.
- Requiere daemon (root o rootless con limitaciones).
- Ecosistema enorme (Docker Hub, Compose, Swarm, Kubernetes).

```bash
# Ejemplo rápido
docker run -d --name web -p 8080:80 nginx:alpine
docker compose up -d
```

# Podman

- Compatible con Docker CLI y Compose (en gran medida).
- **Sin daemon** (daemonless) y rootless por defecto → más seguro.
- Ideal para entornos de desarrollo y servidores donde se quiere evitar root.
- Usa las mismas imágenes OCI que Docker.

```bash
podman run -d --name web -p 8080:80 nginx:alpine
podman compose up -d   # o podman-compose
```

# Cuándo usar cada uno

- **LXC en Proxmox**: servicios de larga vida, bases de datos, servidores tradicionales, aislamiento fuerte sin overhead de KVM.
- **Docker/Podman**: aplicaciones modernas, microservicios, pipelines CI/CD, desarrollo local reproducible.
- **Preferir Podman** cuando se quiera rootless y sin daemon.
- **Preferir Docker** cuando se necesite el ecosistema completo (Swarm, muchas herramientas legacy).

# Buenas prácticas generales

- Nunca ejecutar contenedores como root dentro de la app si es posible.
- Usar volúmenes nombrados o binds controlados para datos persistentes.
- Mantener imágenes actualizadas y escanear vulnerabilidades.
- Limitar recursos (CPU, memoria, pids) con cgroups.
- En Proxmox: preferir LXC para la mayoría de servicios; usar KVM solo cuando se necesite kernel propio o Windows.

# Enlaces útiles

- Documentación LXC: https://linuxcontainers.org/
- Docker: https://docs.docker.com/
- Podman: https://docs.podman.io/

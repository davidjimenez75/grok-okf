---
description: Distribución Linux estable, libre y de referencia. Base de Proxmox VE y de la mayoría de servidores de producción.
generated:
  at: 2026-07-31T07:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - linux
  - debian
  - servidores
  - apt
  - estabilidad
title: Debian
type: Reference
verified:
  at: 2026-07-31T07:35:00Z
  by: human:davidjimenez75
---

# Definición

**Debian** es una de las distribuciones Linux más antiguas, estables y respetadas. Se caracteriza por su compromiso con el software libre, su proceso de liberación riguroso y su enorme repositorio de paquetes.

Es la base de Proxmox VE, Ubuntu, Raspberry Pi OS y de innumerables servidores de producción.

# Versiones relevantes (2026)

- **Debian 12 (Bookworm)**: actual estable (lanzada 2023, soporte hasta ~2028).
- **Debian 13 (Trixie)**: testing / próxima estable.
- **Debian Sid**: unstable (para desarrollo avanzado).

# Gestión de paquetes

```bash
# Actualizar índices y sistema
apt update && apt full-upgrade

# Buscar e instalar
apt search nginx
apt install nginx

# Limpiar
apt autoremove --purge
apt clean

# Ver de dónde viene un paquete
apt-cache policy nginx
```

# Configuración recomendada para servidores

- Usar siempre la rama **stable** en producción.
- Activar actualizaciones de seguridad automáticas con `unattended-upgrades`.
- Preferir paquetes oficiales; usar backports solo cuando sea necesario.
- Mantener `/etc` bajo control de versiones (etckeeper o git).
- Configurar `sources.list` con mirror rápido y security.

# Relación con Proxmox

Proxmox VE se construye sobre Debian. Las actualizaciones del nodo se hacen con `apt` de forma similar, pero hay que respetar las fuentes oficiales de Proxmox para no romper el stack de virtualización.

# Enlaces útiles

- Documentación oficial: https://www.debian.org/doc/
- Wiki: https://wiki.debian.org/
- Security tracker: https://security-tracker.debian.org/

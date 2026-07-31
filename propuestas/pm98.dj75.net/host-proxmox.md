---
description: Configuración recomendada del host Proxmox VE 9.2 para pm98.dj75.net.
generated:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - proxmox
  - host
  - zfs
title: Host Proxmox VE 9.2 — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
---

# Versión objetivo

- **Proxmox VE 9.2** (lanzada 21 de mayo de 2026)
- Basada en Debian 13.5 (Trixie)
- Kernel 7.0 como estable por defecto

# Requisitos mínimos recomendados del hardware

| Recurso        | Mínimo      | Recomendado     |
|----------------|-------------|-----------------|
| CPU            | 16 cores    | 24-32 cores     |
| RAM            | 128 GB      | 192-256 GB      |
| Disco sistema  | 1 TB NVMe   | 2 TB+ NVMe      |
| Backup storage | 4 TB        | 8 TB+ o NAS     |
| Red            | 2× 1 GbE   | 2× 10 GbE      |

# Configuración inicial recomendada

1. Instalación desde ISO oficial de Proxmox VE 9.2.
2. Hostname: `pm98` / FQDN: `pm98.dj75.net`.
3. Configurar repositorios (enterprise o no-subscription).
4. Actualización completa del sistema.
5. Crear pool ZFS (recomendado) o LVM-thin para los guests.
6. Configurar bridges de red (`vmbr0` público/LAN, `vmbr1` interno opcional).
7. Crear token de API con permisos limitados para automatización.
8. Configurar `vzdump` hacia storage de backup externo.
9. Habilitar actualizaciones de seguridad y monitorización básica.

# Almacenamiento

**Opción preferida: ZFS**

- Snapshots nativos y muy rápidos.
- Replicación fácil (`zfs send/receive`).
- Compresión y deduplicación opcionales.

**Alternativa: LVM-thin**

- Más simple si no se necesita la potencia de ZFS.
- Suficiente para muchos escenarios de desarrollo.

# Seguridad del host

- No exponer el puerto 8006 de la GUI a Internet (usar VPN o tunnel).
- Firewall de Proxmox activado.
- Usuarios y tokens con el mínimo privilegio necesario.
- Backups del propio host (configuración `/etc/pve`) además de los guests.

# Referencias relacionadas

- [Proxmox VE](/sistemas/proxmox.md)
- Skill recomendado: [proxmox-ops](/skills/proxmox-ops.md)

---
description: Plataforma de virtualización open-source basada en Debian que combina hipervisor KVM y contenedores LXC con gestión web unificada.
generated:
  at: 2026-07-31T07:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - virtualizacion
  - proxmox
  - kvm
  - lxc
  - homelab
  - servidores
title: Proxmox VE
type: Reference
verified:
  at: 2026-07-31T07:35:00Z
  by: human:davidjimenez75
---

# Definición

**Proxmox Virtual Environment (Proxmox VE)** es una plataforma de virtualización completa, open-source y basada en Debian. Permite gestionar máquinas virtuales (KVM) y contenedores (LXC) desde una interfaz web unificada, con soporte nativo para clustering, almacenamiento compartido, backups y alta disponibilidad.

# Componentes principales

- **KVM**: hipervisor de máquinas virtuales completas (Windows, Linux, BSD…).
- **LXC**: contenedores de sistema (comparten kernel del host, muy ligeros).
- **pve-manager**: interfaz web y API REST.
- **Ceph / ZFS / LVM / directory**: backends de almacenamiento.
- **Corosync + Pacemaker**: clustering y HA.

# Casos de uso típicos

- Homelab y laboratorios de pruebas.
- Servidores de producción con múltiples servicios aislados.
- Entornos de desarrollo y CI/CD.
- Clustering de 2-3 nodos con almacenamiento compartido (Ceph o NFS).

# Comandos útiles rápidos

```bash
# Listar VMs y contenedores
pvesh get /cluster/resources --type vm

# Crear contenedor LXC desde plantilla
pct create 100 local:vztmpl/debian-12-standard_12.2-1_amd64.tar.zst \
  --hostname debian12 --memory 2048 --cores 2 --net0 name=eth0,bridge=vmbr0,ip=dhcp

# Backup de un contenedor
vzdump 100 --storage local --mode snapshot --compress zstd

# Actualizar el nodo
apt update && apt full-upgrade
```

# Buenas prácticas

- Usar **ZFS** o **Ceph** para almacenamiento con snapshots y replicación.
- Separar la red de gestión de la de VMs (bridges distintos).
- Mantener el nodo Proxmox actualizado pero probar upgrades en un nodo de prueba.
- Usar plantillas LXC oficiales y mantenerlas actualizadas.
- Configurar backups automáticos con `vzdump` + retención.
- Para producción: al menos 3 nodos + Quorum + almacenamiento compartido.

# Enlaces útiles

- Documentación oficial: https://pve.proxmox.com/pve-docs/
- Wiki: https://pve.proxmox.com/wiki/Main_Page
- Foro: https://forum.proxmox.com/

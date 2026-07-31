---
description: Procedimiento para realizar y restaurar backups de máquinas virtuales y contenedores en Proxmox VE.
generated:
  at: 2026-07-31T07:50:00Z
  by: human:davidjimenez75
status: stable
tags:
  - playbook
  - backup
  - proxmox
  - recuperacion
title: Backup y restauración en Proxmox
type: Playbook
verified:
  at: 2026-07-31T07:50:00Z
  by: human:davidjimenez75
---

# Objetivo

Garantizar que se pueden recuperar VMs y contenedores de forma rápida y fiable ante fallos de hardware, errores humanos o desastres.

# Tipos de backup en Proxmox

- **Snapshot** (rápido, requiere almacenamiento que lo soporte: ZFS, LVM-thin, Ceph).
- **Suspend** (congela la VM brevemente).
- **Stop** (apaga la VM/CT, más consistente pero con downtime).

Recomendado en producción: **snapshot** + almacenamiento con snapshots nativos.

# Backup manual de un contenedor/VM

```bash
# Backup de CT/VM 100 al storage 'local' con compresión zstd
vzdump 100 --storage local --mode snapshot --compress zstd --notes-template "{{guestname}}-{{vmid}}"

# Ver backups existentes
pvesm list local --content backup
```

# Programar backups (GUI o cron)

En la interfaz web: Datacenter → Backup → Add.

O mediante cron en el nodo:

```cron
# Todos los días a las 02:00, VMs 100-110, retención 7 días
0 2 * * * root vzdump 100 101 102 103 104 105 106 107 108 109 110 \
  --storage local --mode snapshot --compress zstd --maxfiles 7
```

# Restauración

```bash
# Listar backups
pvesm list local --content backup

# Restaurar (crear nuevo CT/VM o sobrescribir)
qmrestore /var/lib/vz/dump/vzdump-qemu-100-....vma.zst 200   # para VM
pct restore 200 /var/lib/vz/dump/vzdump-lxc-100-....tar.zst  # para CT
```

Desde la GUI: seleccionar el backup → Restore.

# Buenas prácticas

- Almacenar backups en un storage distinto al de las VMs (idealmente otro nodo o NAS).
- Probar restauraciones periódicamente (al menos trimestral).
- Usar retención (maxfiles o prune-backups).
- Incluir notas descriptivas en los backups.
- Para datos críticos: combinar con backups a nivel de aplicación (mysqldump, etc.).
- Considerar replicación (ZFS send/receive o Ceph) para RPO bajo.

# Verificación post-restauración

1. Arrancar el CT/VM restaurado.
2. Comprobar conectividad de red.
3. Verificar servicios críticos (web, base de datos…).
4. Comparar con el estado esperado.

# Referencias

- [Proxmox VE](/sistemas/proxmox.md)
- Documentación oficial de vzdump: https://pve.proxmox.com/pve-docs/vzdump.1.html

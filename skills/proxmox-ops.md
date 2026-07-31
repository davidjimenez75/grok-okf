---
description: Skill de agente para gestionar Proxmox VE (VMs, contenedores LXC, backups, clustering y monitorización) de forma segura y automatizada.
generated:
  at: 2026-07-31T08:10:00Z
  by: human:davidjimenez75
status: stable
tags:
  - skill
  - proxmox
  - virtualizacion
  - sysadmin
  - automatizacion
title: proxmox-ops
type: Skill
verified:
  at: 2026-07-31T08:10:00Z
  by: human:davidjimenez75
---

# Por qué te lo recomiendo

Tu perfil gira en torno a **Proxmox** (#proxmox en tu bio). Un skill dedicado te permite que un agente (Grok u otro) realice operaciones cotidianas y de emergencia sin que tengas que recordar cada comando `pct`/`qm`/`vzdump` o entrar a la GUI.

# Capacidades sugeridas

- Listar VMs y contenedores con estado, recursos y tags.
- Crear / clonar / destruir contenedores LXC a partir de plantillas.
- Ejecutar backups bajo demanda (`vzdump`) y listar/restaurar backups existentes.
- Consultar uso de CPU/RAM/disco/red de un nodo o de un guest.
- Gestionar snapshots y migraciones en vivo (si hay cluster).
- Aplicar configuraciones de red (bridges, firewall de Proxmox).
- Generar reportes de salud del cluster.

# Enfoque de implementación

1. **Herramientas base**:
   - CLI de Proxmox (`pvesh`, `pct`, `qm`, `vzdump`) vía SSH o ejecución local.
   - API REST de Proxmox (token de API con permisos mínimos).
2. **Seguridad**:
   - Nunca usar el usuario `root` directamente desde el agente.
   - Tokens de API con roles limitados (PVEVMAdmin, PVEAuditor, etc.).
   - Confirmación humana obligatoria para acciones destructivas (destroy, restore sobreproducción).
3. **Formato de skill**:
   - Un directorio `skills/proxmox-ops/` con `SKILL.md` que describa las herramientas disponibles y ejemplos de uso.
   - Funciones claras: `list_guests`, `create_lxc`, `backup_guest`, `restore_guest`, `node_status`.

# Relación con el resto del bundle

- Se apoya en [Proxmox VE](/sistemas/proxmox.md) y el playbook [Backup y restauración en Proxmox](/playbooks/backup-proxmox.md).
- Complementa el skill [container-ops](container-ops.md) para la parte LXC.

# Prioridad de implementación

**Alta**. Es el skill con mayor retorno inmediato para tu día a día.

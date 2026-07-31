---
description: Estimación de recursos de hardware y software necesarios para pm98.dj75.net con decenas de contenedores.
generated:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - recursos
  - hardware
  - dimensionamiento
title: Estimación de recursos — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
---

# Escenario de referencia

- 25-40 contenedores LXC activos
- 1 VM SQL Server
- 1 CT proxy + 1 CT git
- Carga de desarrollo (no producción intensiva 24/7)

# Hardware recomendado

| Recurso              | Mínimo viable | Cómodo / recomendado |
|----------------------|---------------|------------------------|
| CPU                  | 16 cores      | 24-32 cores            |
| RAM                  | 128 GB        | 192-256 GB             |
| Disco sistema + guests | 2 TB NVMe   | 4 TB NVMe              |
| Storage de backups   | 4 TB          | 8 TB+ o NAS externo    |
| Red                  | 2× 1 GbE     | 2× 10 GbE             |

# Desglose orientativo de RAM

| Componente              | RAM estimada     |
|-------------------------|------------------|
| Host Proxmox + overhead | 8-16 GB          |
| VM SQL Server           | 16-32 GB         |
| 10 CTs .NET/Rust        | 40-60 GB         |
| 10 CTs LAMP/PrestaShop  | 30-50 GB         |
| Resto de CTs + margen   | 20-40 GB         |
| **Total orientativo**   | **120-200 GB**   |

# Almacenamiento

- Los CTs de desarrollo suelen crecer con `node_modules`, `target/`, `vendor/`, bases de datos locales, etc.
- Prever margen generoso y monitorizar el uso del pool ZFS/LVM.
- Los backups ocupan significativamente más que el tamaño en caliente (retención × tamaño).

# Escalado futuro

Si se supera cómodamente el número de CTs o la carga:

1. Añadir más RAM/CPU al mismo nodo (si el hardware lo permite).
2. Pasar a un cluster Proxmox de 2-3 nodos con almacenamiento compartido (Ceph o NFS).
3. Mover los CTs más pesados a nodos dedicados.

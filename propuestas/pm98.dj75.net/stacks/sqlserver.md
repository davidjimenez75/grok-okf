---
description: Recomendación de despliegue de SQL Server para pm98.dj75.net (VM Ubuntu preferida sobre LXC).
generated:
  at: 2026-07-31T08:40:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - sqlserver
  - base-de-datos
  - stack
title: Stack SQL Server — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:40:00Z
  by: human:davidjimenez75
---

# Decisión de arquitectura

**Recomendación fuerte: máquina virtual Ubuntu 24.04 LTS + SQL Server 2025.**

Motivos:

- Soporte oficial de Microsoft (Ubuntu y RHEL).
- Menos problemas con cgroups v2 y sistemas de archivos (ZFS en LXC es especialmente problemático).
- Mayor estabilidad para cargas de desarrollo medianas.

LXC solo se contempla para pruebas muy ligeras y no productivas.

# Configuración recomendada de la VM

| Recurso | Valor orientativo     |
|---------|-----------------------|
| vCPU    | 4-8                   |
| RAM     | 16-32 GB              |
| Disco   | 100-200 GB (XFS/ext4) |
| Red     | vmbr1 (interna) + acceso controlado |

# Instalación (resumen)

1. Crear VM Ubuntu 24.04 desde ISO o cloud-image.
2. Seguir la guía oficial de Microsoft para SQL Server 2025 en Ubuntu.
3. Configurar `mssql-conf` (memoria, puertos, etc.).
4. Crear logins y bases de datos de desarrollo.
5. Restringir el puerto 1433 a la red interna o a IPs de los CTs autorizados.

# Conectividad desde los CTs

- Los CTs .NET y otros se conectan usando el nombre interno `sql.pm98.dj75.net` o la IP de la red `vmbr1`.
- Connection strings almacenados fuera del código (variables de entorno o vault).

# Backups

- Backups de Proxmox de la VM completa (diario).
- Adicionalmente: backups lógicos de bases de datos (`BACKUP DATABASE` o herramientas de Microsoft) con retención propia.

# Alternativa LXC (no recomendada para uso serio)

Solo si se aceptan las limitaciones: LXC privilegiado Ubuntu, sistema de archivos compatible y pruebas exhaustivas de estabilidad.

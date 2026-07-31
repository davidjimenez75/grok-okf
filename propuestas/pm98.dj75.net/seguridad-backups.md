---
description: Política de seguridad y estrategia de backups para el servidor pm98.dj75.net.
generated:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - seguridad
  - backups
  - vzdump
title: Seguridad y backups — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
---

# Principios de seguridad

1. Contenedores **unprivileged** siempre que sea posible.
2. SQL Server en VM aislada (no LXC).
3. Mínimo privilegio en tokens de API de Proxmox.
4. Proxy inverso como único punto de entrada HTTP/S.
5. Secretos (contraseñas, connection strings) fuera del código y de los CTs cuando sea viable (vault o variables de entorno gestionadas).
6. Actualizaciones controladas del host y de las plantillas.

# Backups

## Herramienta principal

`vzdump` nativo de Proxmox.

## Política recomendada

| Tipo de guest      | Frecuencia     | Retención     | Modo      |
|--------------------|----------------|---------------|-----------|
| CT de desarrollo   | Diario         | 7-14 días    | snapshot  |
| CT PrestaShop      | Diario         | 14 días      | snapshot  |
| VM SQL Server      | Diario + semanal | 14 + 4 sem. | snapshot / stop |
| Plantillas         | Tras cambios   | 3-5 versiones | snapshot  |

## Ubicación de los backups

- Storage distinto al de los guests (otro disco, otro nodo o NAS).
- Idealmente fuera del mismo rack físico si es posible.

## Pruebas de restauración

- Realizar una restauración de prueba al menos una vez al trimestre.
- Documentar el tiempo de recuperación (RTO) real.

# Otras medidas

- Fail2ban o equivalente en el CT proxy y en SSH de los CTs.
- Actualizaciones de seguridad automáticas en Debian (`unattended-upgrades`) donde no rompan servicios críticos.
- Revisar periódicamente los logs de Proxmox y de los CTs más expuestos.

# Referencias

- Playbook: [Backup y restauración en Proxmox](/playbooks/backup-proxmox.md)
- Playbook: [Respuesta a incidentes](/playbooks/respuesta-incidentes.md)

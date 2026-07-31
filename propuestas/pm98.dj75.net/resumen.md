---
description: Resumen ejecutivo de la propuesta de implementación del servidor pm98.dj75.net con Proxmox VE 9.2 y contenedores Debian 13 para desarrollo.
generated:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - proxmox
  - debian13
  - desarrollo
title: Resumen ejecutivo — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
---

# Objetivo

Desplegar un servidor de desarrollo llamado **pm98.dj75.net** basado en la última versión estable de Proxmox VE (**9.2**, mayo 2026) con decenas de contenedores LXC **Debian 13 (Trixie)** preparados para los siguientes stacks:

- .NET 10 (LTS)
- SQL Server (recomendado en VM)
- Rust
- PHP / LAMP
- PrestaShop 9.x

# Principios de diseño

- **Aislamiento**: un contenedor (o VM) por proyecto o por stack cuando tenga sentido.
- **Reutilización**: plantillas Debian 13 bien mantenidas.
- **Bajo overhead**: LXC unprivileged siempre que sea posible.
- **Seguridad**: mínimo privilegio, backups automáticos, proxy inverso centralizado.
- **Documentación viva**: todo el diseño queda registrado en este bundle OKF.

# Decisión clave

| Componente     | Tecnología recomendada      | Motivo principal                          |
|----------------|-----------------------------|-------------------------------------------|
| Hipervisor     | Proxmox VE 9.2              | Última estable, basada en Debian 13      |
| Contenedores   | LXC Debian 13.6             | Ligereza + aislamiento suficiente        |
| SQL Server     | VM Ubuntu 24.04             | Mejor soporte oficial y estabilidad       |
| Proxy / SSL    | CT dedicado (Caddy/Nginx)   | Gestión centralizada de dominios         |
| Almacenamiento | ZFS (preferido)             | Snapshots nativos y replicación          |

# Resultado esperado

Un entorno de desarrollo flexible, rápido de provisionar y fácil de respaldar, capaz de albergar decenas de proyectos simultáneos sin degradar el rendimiento del host.

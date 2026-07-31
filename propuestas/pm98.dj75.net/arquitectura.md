---
description: Arquitectura lógica y física propuesta para el servidor pm98.dj75.net.
generated:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - arquitectura
  - proxmox
  - lxc
title: Arquitectura general — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
---

# Vista general

```
pm98.dj75.net (Proxmox VE 9.2)
│
├── Storage: ZFS pool (o LVM-thin)
├── Red: vmbr0 (LAN/pública) + vmbr1 (interna opcional)
│
├── Plantilla base: debian-13-dev (unprivileged)
│
├── Grupo .NET 10
│   ├── ct-dotnet-dev-XX
│   └── ct-dotnet-api-XX
│
├── Grupo Rust
│   └── ct-rust-dev-XX
│
├── Grupo LAMP / PrestaShop
│   ├── ct-lamp-base-XX
│   └── ct-prestashop-XX
│
├── Utilidades
│   ├── ct-proxy          (Caddy o Nginx + Let’s Encrypt)
│   ├── ct-git            (Forgejo / Gitea)
│   └── ct-monitoring     (opcional)
│
└── VM dedicada
    └── vm-sqlserver      (Ubuntu 24.04 + SQL Server 2025)
```

# Decisiones de diseño

- **LXC para casi todo**: bajo consumo de recursos y arranque rápido.
- **VM solo para SQL Server**: evita problemas conocidos de cgroups, sistema de archivos y soporte oficial de Microsoft en LXC.
- **Plantillas**: una plantilla Debian 13 bien cuidada + plantillas derivadas por stack.
- **Proxy central**: un único punto de entrada HTTPS que enruta a los distintos CTs por subdominio.
- **Red interna opcional**: útil para que los CTs hablen entre sí sin exponer puertos al exterior.

# Flujo de acceso típico

1. Usuario accede a `https://ps-tienda1.pm98.dj75.net`
2. El CT proxy termina SSL y reenvía al CT PrestaShop correspondiente
3. El CT PrestaShop consulta la base de datos (local o en la VM SQL Server según el caso)

# Escalabilidad

La arquitectura permite añadir nuevos CTs en minutos a partir de plantillas. El límite real lo marca la RAM y el almacenamiento del host, no el número de contenedores en sí.

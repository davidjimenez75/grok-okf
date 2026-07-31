---
description: Diseño de red, bridges, DNS y proxy inverso para pm98.dj75.net.
generated:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - red
  - dns
  - proxy
  - ssl
title: Red y DNS — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
---

# Bridges de Proxmox

| Bridge | Uso                              | Notas                          |
|--------|----------------------------------|--------------------------------|
| vmbr0  | LAN / acceso público            | Interfaz principal del host    |
| vmbr1  | Red interna entre CTs y VM SQL   | Opcional pero muy recomendable |

# Esquema de nombres DNS

Dominio base: **pm98.dj75.net**

| Subdominio / patrón              | Destino                     |
|----------------------------------|-----------------------------|
| `pm98.dj75.net`                  | GUI Proxmox (solo VPN)      |
| `*.pm98.dj75.net`                | CT proxy (catch-all)        |
| `sql.pm98.dj75.net`              | VM SQL Server               |
| `git.pm98.dj75.net`              | CT Forgejo/Gitea            |
| `ps-<tienda>.pm98.dj75.net`      | CT PrestaShop correspondiente |
| `api-<proyecto>.pm98.dj75.net`   | CT .NET API                 |
| `dev-<proyecto>.pm98.dj75.net`   | CT de desarrollo genérico  |

# Proxy inverso

Se recomienda un CT dedicado (`ct-proxy`) con **Caddy** o **Nginx**.

Ventajas:

- Terminación SSL centralizada (Let’s Encrypt automático)
- Un solo punto de entrada
- Fácil añadir nuevos proyectos sin tocar firewalls externos
- Posibilidad de autenticación adicional (Authelia, basic auth, etc.)

# Resolución interna

- Los CTs deben poder resolver tanto los nombres públicos como los nombres internos de la red `vmbr1`.
- Opciones: DNS del router, CoreDNS/Unbound en un CT, o entradas en `/etc/hosts` de cada contenedor (menos escalable).

# Firewall

- Puerto 8006 (GUI Proxmox) solo accesible desde VPN o red de gestión.
- Puertos 80/443 abiertos hacia el CT proxy.
- Puerto 1433 (SQL Server) solo accesible desde la red interna o desde CTs autorizados.
- Resto de puertos cerrados por defecto.

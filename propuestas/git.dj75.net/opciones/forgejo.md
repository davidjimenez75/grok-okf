---
description: Forgejo (y Gitea) como forge Git ligero con interfaz web completa, issues, pull requests y más.
generated:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - forgejo
  - gitea
  - web-ui
title: Forgejo / Gitea — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
---

# Resumen

**Forgejo** es el fork comunitario activo de Gitea. Ambos ofrecen una experiencia tipo GitHub (repos, issues, PRs, wiki, packages, Actions…) en un binario Go relativamente ligero. En 2026 se recomienda preferir Forgejo por su gobernanza comunitaria.

# Requisitos de recursos (Q1900M)

| RAM del sistema | ¿Viable? | Comentario |
|-----------------|----------|------------|
| 4 GB            | Condicional | Solo con SQLite + features recortadas. Ajustado. |
| **8 GB**        | **Sí, cómodo** | Recomendado. Holgado para uso personal/familiar. |
| 16 GB           | Sí, de sobra | Margen amplio + runners ligeros. |

Uso típico en reposo (SQLite, sin Actions): **150–400 MB**.

# Ajustes recomendados en hardware limitado

- Base de datos: **SQLite** (nunca PostgreSQL/MySQL en este hardware).
- Desactivar o limitar: Actions, Packages, LFS (si no se usa), mirror, search avanzado.
- Reducir número de workers / concurrencia en `app.ini`.
- Escuchar solo en `127.0.0.1:3000` y poner un proxy inverso ligero (Caddy o nginx).
- SSD altamente recomendado.

# Instalación orientativa (Debian 13)

1. Descargar el binario oficial de Forgejo (o paquete si está disponible).
2. Crear usuario `git` o `forgejo`.
3. Configurar `app.ini` (ruta de datos, SQLite, dominio, SSH puerto, etc.).
4. Crear servicio systemd.
5. (Opcional) Caddy/nginx como proxy + TLS interno o Let’s Encrypt si se expone.

Ejemplo mínimo de `app.ini` (extracto):

```ini
[database]
DB_TYPE = sqlite3
PATH = /var/lib/forgejo/data/forgejo.db

[server]
DOMAIN = git.dj75.net
HTTP_ADDR = 127.0.0.1
HTTP_PORT = 3000
ROOT_URL = https://git.dj75.net/
SSH_PORT = 22

[repository]
ROOT = /var/lib/forgejo/data/repositories
```

# Ventajas

- UI web completa y familiar.
- Issues, Pull Requests, wiki, webhooks, etc.
- Consumo de recursos razonable (mucho más ligero que GitLab).
- Activo y bien mantenido (Forgejo).

# Desventajas

- Más superficie de ataque y mantenimiento que las opciones solo-SSH.
- En 4 GB hay que recortar funcionalidades.
- El J1900 sigue siendo un CPU modesto para operaciones pesadas.

# Cuándo elegirla

- Se necesita interfaz web tipo GitHub.
- Se dispone de **al menos 8 GB de RAM** (recomendado).
- Uso personal, familiar o pequeño equipo.

# Relación con otros documentos

- [Comparativa general](../opciones.md)
- [Recursos](../recursos.md)
- [Arquitectura](../arquitectura.md)

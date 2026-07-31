---
description: Servidor Git moderno de Charmbracelet con TUI accesible por SSH y gestión sencilla de repositorios.
generated:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - soft-serve
  - charmbracelet
  - tui
title: Soft Serve — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
---

# Resumen

Soft Serve es un servidor Git escrito en Go por Charmbracelet. Ofrece una TUI agradable accesible por SSH, creación de repositorios bajo demanda, gestión de usuarios/colaboradores y soporte de LFS. Todo en un único binario.

# Requisitos de recursos (Q1900M)

| Recurso     | Uso aproximado          |
|-------------|-------------------------|
| RAM         | 20–60 MB (idle)         |
| CPU         | Bajo                    |
| Disco base  | ~30 MB + datos          |
| Compatible con 4 GB | **Sí (excelente)** |

# Características principales

- TUI navegable sobre SSH (listar repos, ver ficheros, commits…).
- Clone/push por SSH, HTTP y protocolo Git.
- Creación de repos con `git push` o comandos SSH.
- Colaboradores con niveles de acceso (read-only / read-write).
- Git LFS, webhooks y hooks del lado del servidor.
- Base de datos SQLite por defecto.

# Instalación orientativa (Debian 13)

Opciones comunes:

1. **Binario desde releases** de GitHub (`charmbracelet/soft-serve`).
2. **Paquete** si se añade el repositorio de Charm (apt).
3. **Go**: `go install github.com/charmbracelet/soft-serve/cmd/soft@latest`

Ejemplo de servicio systemd mínimo:

```ini
[Unit]
Description=Soft Serve Git server
After=network.target

[Service]
Type=simple
User=softserve
WorkingDirectory=/var/lib/soft-serve
ExecStart=/usr/local/bin/soft serve
Restart=on-failure
Environment=SOFT_SERVE_DATA_PATH=/var/lib/soft-serve
Environment=SOFT_SERVE_INITIAL_ADMIN_KEYS="ssh-ed25519 AAAA... tu-clave"

[Install]
WantedBy=multi-user.target
```

Puerto SSH por defecto: **23231** (configurable).

Acceso a la TUI:

```bash
ssh git.dj75.net -p 23231
```

# Ventajas

- Experiencia de usuario moderna y agradable.
- Muy ligero.
- Instalación simple (un binario).
- Crear repos es inmediato.

# Desventajas

- Control de acceso menos granular que Gitolite (no llega a nivel de rama/fichero con la misma potencia).
- Proyecto más joven (aunque activo y estable en 2026).
- Sin interfaz web clásica (solo TUI).

# Cuándo elegirla

- Se quiere una experiencia moderna sin montar una aplicación web completa.
- Uso personal o pequeño grupo.
- Se valora especialmente la TUI y la facilidad de gestión desde terminal.

# Relación con otros documentos

- [Comparativa general](../opciones.md)
- [Arquitectura](../arquitectura.md)
- [Red y DNS](../red-dns.md) (puerto 23231)

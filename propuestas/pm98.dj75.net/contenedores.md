---
description: Estrategia de creación, plantillas y gestión de contenedores LXC Debian 13 en pm98.dj75.net.
generated:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - lxc
  - debian13
  - contenedores
  - plantillas
title: Estrategia de contenedores — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:30:00Z
  by: human:davidjimenez75
---

# Principio general

Todos los entornos de desarrollo (salvo SQL Server) viven en **contenedores LXC unprivileged** basados en **Debian 13.6 (Trixie)**.

# Plantilla base

Nombre propuesto: `debian-13-dev`

Contenido mínimo recomendado:

- Sistema actualizado
- `curl`, `wget`, `git`, `vim`, `htop`, `sudo`, `ca-certificates`, `locales`
- Usuario de desarrollo con sudo
- Zona horaria y locale en `es_ES.UTF-8`
- SSH habilitado con autenticación por clave

# Plantillas derivadas (opcionales pero muy útiles)

| Plantilla              | Uso principal                     |
|------------------------|-----------------------------------|
| `debian13-dotnet`      | .NET 10 SDK + herramientas        |
| `debian13-rust`        | rustup + toolchain estable        |
| `debian13-lamp`        | Apache + PHP 8.4 + MariaDB        |
| `debian13-prestashop`  | LAMP optimizado para PrestaShop   |

# Convención de nombres

```
ct-<stack>-<proyecto|dev>-<número>
```

Ejemplos reales:

- `ct-dotnet-miapi-01`
- `ct-rust-cli-02`
- `ct-prestashop-tienda1`
- `ct-lamp-dev-03`
- `ct-proxy`
- `ct-git`

# Recursos orientativos por tipo

| Tipo de CT       | vCPU | RAM    | Disco    |
|------------------|------|--------|----------|
| .NET 10          | 2-4  | 4-8 GB | 40-80 GB |
| Rust             | 2-4  | 4-8 GB | 40-60 GB |
| LAMP base        | 2    | 2-4 GB | 30 GB    |
| PrestaShop       | 2-4  | 4-6 GB | 40-60 GB |
| Proxy / utilidades | 1-2 | 1-2 GB | 15-30 GB |

# Ciclo de vida recomendado

1. Crear a partir de plantilla (clone o `pct create` desde template).
2. Ajustar recursos y red.
3. Instalar software específico del stack.
4. Documentar el CT (propósito, puertos, dependencias).
5. Incluir en el plan de backups.
6. Destruir cuando ya no se necesite (tras backup final).

# Buenas prácticas

- Preferir siempre contenedores **unprivileged**.
- No compartir el mismo CT entre proyectos no relacionados.
- Mantener la plantilla base actualizada y volver a generar las derivadas periódicamente.
- Usar tags de Proxmox (`dotnet`, `rust`, `prestashop`, `prod-dev`, etc.) para filtrar fácilmente.

# Referencias

- [Contenedores](/sistemas/contenedores.md)
- [Debian](/sistemas/debian.md)
- Skill: [container-ops](/skills/container-ops.md)

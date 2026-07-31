---
description: Diseño de scripts de instalación, verificación y actualización, y de los comandos CLI instalados preferentemente en /usr/local/bin.
generated:
  at: 2026-07-31T23:29:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - scripts
  - cli
  - usr-local-bin
title: Scripts y comandos — Mono-repo unificado de servidor + OKF
type: Reference
verified:
  at: 2026-07-31T23:29:00Z
  by: agent:grok
---

# Principios de los scripts

- **Idempotentes**: se pueden ejecutar varias veces sin efectos secundarios no deseados.
- **Legibles por agentes**: salida estructurada (texto claro o JSON opcional) y códigos de salida estándar.
- **Documentados**: cada script tiene un encabezado con uso, opciones y ejemplos.
- **Independientes del path de instalación** cuando sea posible (usan variables o detectan el repo).

# Scripts principales (`scripts/`)

| Script            | Propósito                                                                 |
|-------------------|---------------------------------------------------------------------------|
| `bootstrap.sh`    | Primera instalación: crea enlaces, instala dependencias mínimas, genera configs |
| `install.sh`      | Instala o actualiza componentes específicos (web, dependencias, etc.)     |
| `verify.sh`       | Comprueba salud del sistema, presencia de binarios, conformidad OKF       |
| `update.sh`       | Aplica cambios del repo (git pull + re-enlace + recarga de servicios)     |
| `backup.sh`       | Copia de seguridad de datos críticos + estado del conocimiento            |

# Comandos CLI (`bin/` → `/usr/local/bin`)

Preferencia del usuario: **`/usr/local/bin`** (estándar FHS para software local, no gestionado por el gestor de paquetes).

## Prefijo `okf-` (conocimiento)

- `okf-view <concepto>` — muestra un concepto (frontmatter + body)
- `okf-search <término>` — búsqueda simple en títulos, tags y cuerpos
- `okf-validate` — ejecuta el validador de conformidad OKF v0.2
- `okf-index` — regenera o muestra los `index.md`
- `okf-log` — añade una entrada a `log.md` (útil para agentes)

## Prefijo `srv-` (operaciones del servidor)

- `srv-status` — estado general (servicios, disco, últimos cambios OKF)
- `srv-verify` — wrapper de `scripts/verify.sh`
- `srv-update` — wrapper de `scripts/update.sh`
- `srv-backup` — wrapper de `scripts/backup.sh`

# Mecanismo de instalación de binarios

```bash
# Dentro de bootstrap.sh / install.sh
REPO_ROOT="$(cd "$(dirname "$0")/.." && pwd)"
for cmd in "$REPO_ROOT"/bin/*; do
  name=$(basename "$cmd")
  ln -sfn "$cmd" "/usr/local/bin/$name"
done
```

Ventajas de enlaces simbólicos:

- Los cambios en el repo se reflejan inmediatamente.
- Fácil de desinstalar (`rm /usr/local/bin/okf-* /usr/local/bin/srv-*`).
- No requiere `sudo` si el usuario tiene permisos de escritura en `/usr/local/bin` (o se usa un directorio alternativo).

# Alternativas a `/usr/local/bin`

Ver documento [Opciones de ubicación de binarios](opciones-binarios.md).

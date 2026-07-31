---
description: Análisis de ubicaciones posibles para los comandos CLI del monorepo, con preferencia por /usr/local/bin y alternativas abiertas.
generated:
  at: 2026-07-31T23:33:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - binarios
  - usr-local-bin
  - fhs
title: Opciones de ubicación de binarios — Mono-repo unificado
type: Reference
verified:
  at: 2026-07-31T23:33:00Z
  by: agent:grok
---

# Preferencia del usuario

**`/usr/local/bin`** — es la ubicación clásica FHS para software instalado localmente (no gestionado por `apt`/`dpkg`).

# Comparativa de opciones

| Ubicación              | Ventajas                                      | Desventajas                                      | Cuándo usarla                          |
|------------------------|-----------------------------------------------|--------------------------------------------------|----------------------------------------|
| `/usr/local/bin`       | Estándar, visible en PATH de la mayoría de usuarios, no interferido por paquetes | Requiere permisos de escritura (sudo o grupo)   | **Opción por defecto**                 |
| `~/.local/bin`         | No necesita root, XDG compliant               | Solo disponible para el usuario concreto         | Entornos multi-usuario o sin sudo      |
| `/opt/okf/bin`         | Aislado, fácil de borrar completo             | Hay que añadir al PATH manualmente               | Instalaciones “paquete local”          |
| `/usr/bin`             | Máxima visibilidad                            | Riesgo de colisión con paquetes del sistema      | Evitar                                |
| Contenedor / Nix / Guix| Reproducibilidad total                        | Más complejidad                                  | Cuando se adopte ese paradigma         |

# Recomendación práctica

1. **Por defecto**: enlaces simbólicos desde el monorepo hacia `/usr/local/bin`.
2. **Si no hay permisos**: detectar y caer a `~/.local/bin` (y avisar al usuario de añadirla al PATH si no está).
3. **Opción explícita**: variable de entorno `OKF_BIN_DIR` o flag `--bin-dir` en `bootstrap.sh`.

Ejemplo de lógica en bootstrap:

```bash
BIN_DIR="${OKF_BIN_DIR:-/usr/local/bin}"
if [[ ! -w "$BIN_DIR" ]]; then
  BIN_DIR="$HOME/.local/bin"
  mkdir -p "$BIN_DIR"
  echo "Usando $BIN_DIR (sin permisos de escritura en /usr/local/bin)"
fi
```

# Desinstalación limpia

```bash
rm -f /usr/local/bin/okf-* /usr/local/bin/srv-*
# o el directorio alternativo elegido
```

Con enlaces simbólicos, desinstalar es trivial y no deja basura de binarios compilados.

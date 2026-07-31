---
description: Fases concretas y priorizadas para convertir el monorepo (o evolucionar grok-okf) en el sistema unificado de operaciones + OKF + web + agentes.
generated:
  at: 2026-07-31T23:32:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - plan
  - implementacion
title: Plan de implementación — Mono-repo unificado de servidor + OKF
type: Reference
verified:
  at: 2026-07-31T23:32:00Z
  by: agent:grok
---

# Fase 0 — Preparación (1-2 días)

- Decidir si se evoluciona el repo actual `grok-okf` o se crea un repo nuevo que lo importe.
- Crear la estructura de directorios (`scripts/`, `bin/`, `configs/`, `web/`, `agents/`).
- Añadir esta propuesta completa y actualizar `propuestas/index.md` + `log.md`.

# Fase 1 — Capa de operaciones mínima (2-4 días)

- Implementar `scripts/bootstrap.sh`, `verify.sh` y `update.sh` (idempotentes).
- Crear 3-5 comandos iniciales en `bin/` (`okf-validate`, `srv-status`, `srv-verify`, `srv-update`).
- Enlazarlos a `/usr/local/bin` desde bootstrap.
- Añadir tests básicos en `tests/`.

# Fase 2 — Enriquecimiento OKF (continuo)

- Crear directorios `tareas/`, `ideas/`, `diagramas/`, `mapas-mentales/`, `infraestructura/`.
- Migrar o crear conceptos de infraestructura real (enlazando con pm98 y git.dj75).
- Mantener `log.md` al día.

# Fase 3 — Servidor web (3-7 días)

- Elegir PHP ligero como primera implementación.
- Implementar parser de frontmatter + render de markdown + endpoint de grafo.
- Añadir viewer interactivo (Cytoscape o equivalente).
- Desplegar en un contenedor Debian 13 del entorno pm98 o en el host de docs.

# Fase 4 — Agentes (paralelo a las anteriores)

- Rellenar `agents/grok-build/`, `agents/claude-code/`, etc. con SYSTEM.md y prompts de ejemplo.
- Definir la política de confianza (empezar en nivel 1 = solo PRs).
- Probar un ciclo completo: agente detecta gap → genera concepto → actualiza log → abre PR.

# Fase 5 — Hardening y automatización

- Cron o systemd timer que ejecute `srv-verify` y notifique.
- Backup automatizado del monorepo + datos del servidor web.
- Documentar el procedimiento de disaster recovery.

# Criterios de éxito

- Un nodo nuevo puede quedar operativo con un solo `bootstrap.sh`.
- Los comandos en `/usr/local/bin` funcionan y son descubribles.
- El conocimiento OKF es navegable por web y por CLI.
- Al menos un agente puede proponer cambios útiles de forma autónoma.
- El `log.md` refleja tanto cambios humanos como de agentes.

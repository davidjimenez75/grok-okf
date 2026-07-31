---
description: Layout de directorios y convenciones del monorepo unificado (scripts, bin, okf, docs, web, agentes).
generated:
  at: 2026-07-31T23:28:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - estructura
  - okf
title: Estructura del repositorio — Mono-repo unificado de servidor + OKF
type: Reference
verified:
  at: 2026-07-31T23:28:00Z
  by: agent:grok
---

# Layout propuesto

```
mono-repo-servidor/   (o el propio grok-okf evolucionado)
├── README.md
├── index.md                  # OKF root index (okf_version: "0.2")
├── log.md                    # historial de cambios del conocimiento + ops
│
├── scripts/                  # scripts de operaciones (bash/python)
│   ├── bootstrap.sh          # instalación inicial + enlaces a /usr/local/bin
│   ├── install.sh
│   ├── verify.sh
│   ├── update.sh
│   ├── backup.sh
│   └── lib/                  # funciones compartidas
│
├── bin/                      # comandos que se instalan en /usr/local/bin
│   ├── okf-view
│   ├── okf-search
│   ├── okf-validate
│   ├── srv-status
│   ├── srv-verify
│   ├── srv-update
│   └── ...
│
├── configs/                  # plantillas de configuración
│   ├── systemd/
│   ├── cron/
│   └── nginx-or-caddy/
│
├── okf/                      # (o la raíz misma) bundle de conocimiento
│   ├── conceptos/
│   ├── sistemas/
│   ├── propuestas/
│   ├── playbooks/
│   ├── tareas/
│   ├── ideas/
│   ├── diagramas/
│   ├── mapas-mentales/
│   ├── infraestructura/
│   ├── metricas/
│   └── skills/
│
├── web/                      # código del servidor web de documentación
│   ├── public/               # estáticos / entrypoint
│   ├── src/                  # lógica PHP (si se elige PHP)
│   ├── templates/
│   └── viewer/               # visualizador de grafo OKF (Cytoscape o similar)
│
├── agents/                   # prompts, skills y reglas para agentes autónomos
│   ├── grok-build/
│   ├── claude-code/
│   ├── opencode/
│   └── codex/
│
├── tests/                    # tests de scripts y de conformidad OKF
└── docs/                     # documentación humana adicional (opcional)
```

# Convenciones

- **Todo el conocimiento** vive en formato OKF v0.2 (frontmatter + markdown).
- Los scripts son **idempotentes** y reportan estado de forma legible por agentes.
- Los binarios de `bin/` son wrappers finos o scripts que se copian/enlazan a `/usr/local/bin`.
- `log.md` se actualiza tanto por humanos como por agentes (entradas más recientes primero).
- Diagramas y mapas mentales se almacenan como markdown (Mermaid, ASCII, o enlaces a SVG generados).
- La carpeta `agents/` contiene instrucciones específicas para cada runtime de agente, de forma que cualquiera pueda tomar el control del mantenimiento.

# Relación con el repo actual

El repositorio `davidjimenez75/grok-okf` ya contiene la mayor parte de la capa OKF. Esta propuesta sugiere:

1. Añadir las capas `scripts/`, `bin/`, `configs/`, `web/` y `agents/`.
2. O crear un nuevo repo que importe/submodule el conocimiento actual y añada las capas operativas.

Ambas opciones son válidas; la primera es más simple para empezar.

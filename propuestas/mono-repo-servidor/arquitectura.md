---
description: Arquitectura en capas del monorepo unificado (operaciones, conocimiento OKF, servidor web y agentes) y flujos de trabajo recomendados.
generated:
  at: 2026-07-31T23:27:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - arquitectura
  - okf
title: Arquitectura general — Mono-repo unificado de servidor + OKF
type: Reference
verified:
  at: 2026-07-31T23:27:00Z
  by: agent:grok
---

# Capas del monorepo

```
┌─────────────────────────────────────────────────────────────┐
│  Capa 4 — Agentes autónomos                                 │
│  (Grok Build · Claude Code · OpenCode · Codex · …)          │
│  Leen OKF, proponen cambios, generan diagramas, verifican   │
└─────────────────────────────────────────────────────────────┘
                              ▲
┌─────────────────────────────────────────────────────────────┐
│  Capa 3 — Servidor web                                      │
│  PHP/LAMP  o  servidor estático + viewer OKF                │
│  Sirve documentación, grafo de conceptos, búsqueda          │
└─────────────────────────────────────────────────────────────┘
                              ▲
┌─────────────────────────────────────────────────────────────┐
│  Capa 2 — Conocimiento OKF                                  │
│  conceptos/ · sistemas/ · propuestas/ · playbooks/ ·        │
│  tareas/ · ideas/ · diagramas/ · mapas-mentales/ · log.md   │
└─────────────────────────────────────────────────────────────┘
                              ▲
┌─────────────────────────────────────────────────────────────┐
│  Capa 1 — Operaciones                                       │
│  scripts/ (install · verify · update · backup)              │
│  bin/ → /usr/local/bin (okf-* · srv-*)                      │
│  configs/ · systemd units · cron                            │
└─────────────────────────────────────────────────────────────┘
```

# Flujos principales

## Bootstrap de un nodo nuevo

1. `git clone` del monorepo
2. `./scripts/bootstrap.sh` (instala dependencias, enlaza binarios a `/usr/local/bin`, genera configs)
3. `srv-verify` (chequeo de salud)
4. (Opcional) levantar el servidor web de docs

## Actualización diaria / semanal

1. `git pull` (o el agente hace el pull)
2. `srv-update` (aplica cambios de scripts, configs y conocimiento)
3. Agentes revisan `log.md`, generan nuevas tareas o diagramas si detectan drift

## Consulta de conocimiento

- Humanos: web (PHP o estático) o `okf-view concepto`
- Agentes: leen directamente los `.md` + frontmatter (OKF v0.2)

# Integración con entornos existentes

- Compatible con la propuesta [pm98.dj75.net](/propuestas/pm98.dj75.net/) (contenedores Debian 13).
- Compatible con [git.dj75.net](/propuestas/git.dj75.net/) como origen o espejo del monorepo.
- El propio `grok-okf` puede evolucionar hacia este monorepo o servir de seed.

# Decisiones clave de arquitectura

| Decisión                    | Recomendación inicial                          | Alternativa aceptable              |
|-----------------------------|------------------------------------------------|------------------------------------|
| Ubicación de binarios       | `/usr/local/bin`                               | `~/.local/bin` o `/opt/okf/bin`    |
| Servidor web                | PHP ligero (LAMP) o Caddy/Nginx estático       | Servidor propio en Go/Rust         |
| Formato de conocimiento     | OKF v0.2 (markdown + YAML)                     | —                                  |
| Mantenimiento               | Agentes + PRs + `log.md`                       | Solo humanos                       |
| Idempotencia de scripts     | Obligatoria                                    | —                                  |

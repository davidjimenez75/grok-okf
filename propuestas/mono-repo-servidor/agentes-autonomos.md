---
description: Cómo usar Grok Build, Claude Code, OpenCode, Codex y otros agentes como mantenedores autónomos del monorepo (scripts, OKF, docs y servidor web).
generated:
  at: 2026-07-31T23:31:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - agentes
  - grok-build
  - claude-code
  - opencode
  - codex
title: Agentes autónomos de mantenimiento — Mono-repo unificado
type: Reference
verified:
  at: 2026-07-31T23:31:00Z
  by: agent:grok
---

# Visión

El monorepo no se mantiene solo por humanos. Se diseña para que **agentes de codificación** puedan:

- Leer el conocimiento OKF y los scripts.
- Detectar drift (conocimiento desactualizado, scripts rotos, diagramas incompletos).
- Proponer o aplicar cambios (PRs o commits directos según la política).
- Actualizar `log.md`.
- Generar o regenerar diagramas, mapas mentales y `index.md`.
- Ejecutar `srv-verify` y reportar estado.

# Agentes contemplados

| Agente          | Fortalezas principales                              | Uso recomendado en el monorepo                  |
|-----------------|-----------------------------------------------------|-------------------------------------------------|
| **Grok Build**  | Contexto largo, razonamiento, integración xAI/OKF   | Autoría de conocimiento OKF, propuestas, revisión |
| **Claude Code** | Edición precisa de código, tool use fuerte          | Refactor de scripts, generación de PHP, tests   |
| **OpenCode**    | (según implementación) edición y ejecución          | Tareas de código y verificación                 |
| **Codex**       | Generación de código y scripts                      | Scaffolding de binarios y scripts nuevos        |

# Carpeta `agents/`

Cada subdirectorio contiene:

- `SYSTEM.md` o `AGENTS.md` con instrucciones específicas para ese runtime.
- Prompts de ejemplo para tareas recurrentes ("actualiza el log", "genera diagrama de infraestructura", "verifica conformidad OKF").
- Reglas de estilo (español de España, frontmatter alfabético, enlaces absolutos bundle-relative, etc.).

Ejemplo de flujo autónomo:

1. Agente clona o hace pull del monorepo.
2. Lee `index.md` + `log.md` + skills relevantes.
3. Ejecuta `okf-validate` y `srv-verify`.
4. Detecta gaps (concepto sin diagrama, script sin test, propuesta sin plan de implementación).
5. Crea o actualiza ficheros OKF y scripts.
6. Añade entrada a `log.md`.
7. Abre PR o hace commit (según configuración de confianza).

# Políticas de confianza

- **Nivel 1 (recomendado al inicio)**: el agente solo propone PRs; un humano revisa y mergea.
- **Nivel 2**: el agente puede hacer commit directo en ramas de trabajo y actualizar `log.md`.
- **Nivel 3**: el agente puede ejecutar `srv-update` y reiniciar servicios (solo en entornos de desarrollo controlados).

# Integración con el skill okf

El skill `okf` ya existente en el entorno Grok se convierte en la fuente de verdad de cómo escribir conceptos. Los demás agentes deben respetar las mismas convenciones (type obligatorio, actor convention, enlaces `/ruta.md`, etc.).

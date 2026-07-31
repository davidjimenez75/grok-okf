---
description: Formato abierto de conocimiento (Open Knowledge Format) diseñado para ser legible por humanos y agentes, basado en markdown con frontmatter YAML.
generated:
  at: 2026-07-31T07:30:00Z
  by: human:davidjimenez75
status: stable
tags:
  - formato
  - conocimiento
  - okf
  - agentes
  - markdown
title: OKF
type: Reference
verified:
  at: 2026-07-31T07:30:00Z
  by: human:davidjimenez75
---

# Definición

**Open Knowledge Format (OKF)** es una especificación abierta (v0.2) para representar conocimiento de forma portable, legible por humanos y consumible por agentes de IA. Se basa en un árbol de archivos markdown con frontmatter YAML.

No requiere esquemas centralizados, ni herramientas propietarias. Si puedes hacer `cat` de un archivo o clonar un repositorio git, puedes usar OKF.

# Características principales

- **Mínimo y portable**: solo markdown + YAML.
- **Proveniencia y confianza**: campos `generated`, `verified`, `sources`, `status` y `stale_after`.
- **Jerarquía y enlaces**: estructura de directorios + enlaces markdown estándar.
- **Tipos de concepto**: `Reference`, `Playbook`, `Metric`, `Attested Computation`, etc. (extensibles).
- **Index y log**: `index.md` para divulgación progresiva y `log.md` para historial.

# Estructura de un bundle

```
bundle/
  index.md          # Índice raíz (opcional, con okf_version)
  log.md            # Historial de cambios
  conceptos/
    index.md
    concepto.md
  playbooks/
    ...
```

# Relación con Grok y xAI

Grok puede consumir y generar bundles OKF, lo que facilita el intercambio de conocimiento estructurado entre agentes y humanos. Este propio repositorio es un ejemplo de bundle OKF.

# Referencias

- Especificación oficial: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
- Repositorio de ejemplo y herramientas: https://github.com/GoogleCloudPlatform/knowledge-catalog

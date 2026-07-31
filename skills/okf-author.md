---
description: Skill de agente para crear, validar, actualizar y mantener bundles de conocimiento en Open Knowledge Format (OKF) v0.2.
generated:
  at: 2026-07-31T08:15:00Z
  by: human:davidjimenez75
status: stable
tags:
  - skill
  - okf
  - conocimiento
  - grafos
  - documentacion
title: okf-author
type: Skill
verified:
  at: 2026-07-31T08:15:00Z
  by: human:davidjimenez75
---

# Por qué te lo recomiendo

Estás construyendo activamente este bundle **grok-okf** y explorando el formato OKF. Un skill especializado acelera la creación de nuevos conceptos, mantiene la consistencia del frontmatter, actualiza los `index.md` y valida que todo siga la especificación v0.2.

# Capacidades sugeridas

- Crear un nuevo concepto con frontmatter ordenado alfabéticamente y plantilla de cuerpo.
- Validar que un archivo cumple OKF v0.2 (type obligatorio, frontmatter parseable, etc.).
- Actualizar automáticamente los `index.md` de un directorio tras añadir/eliminar conceptos.
- Añadir entradas al `log.md` con el formato correcto.
- Detectar enlaces rotos dentro del bundle.
- Generar un resumen del grafo de conocimiento (nodos + aristas principales).
- Convertir notas sueltas o README en conceptos OKF bien estructurados.

# Enfoque de implementación

1. Trabajar directamente sobre el repositorio git (usar el skill de GitHub o git local).
2. Parsear y escribir YAML de frontmatter de forma robusta (ordenar claves alfabéticamente).
3. Respetar la convención de actor `human:davidjimenez75` o `agent/...`.
4. Ofrecer modo «dry-run» antes de escribir cambios.
5. Integrarse con el skill [impact-analysis](impact-analysis.md) para avisar de consecuencias de un cambio.

# Relación con el resto del bundle

- Se apoya en [OKF](/conceptos/okf.md) y [OKF como grafo](/ingenieria-grafos/okf-como-grafo.md).
- Es el skill «meta» que mantiene sano este propio repositorio.

# Prioridad de implementación

**Alta**. Te ahorrará mucho tiempo a medida que el bundle crezca.

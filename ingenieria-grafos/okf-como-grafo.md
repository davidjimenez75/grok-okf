---
description: Un bundle OKF es inherentemente un grafo de conocimiento donde los conceptos son nodos y los enlaces markdown son aristas dirigidas.
generated:
  at: 2026-07-31T07:45:00Z
  by: human:davidjimenez75
status: stable
tags:
  - grafos
  - okf
  - conocimiento
  - graph-engineering
title: OKF como grafo
type: Reference
verified:
  at: 2026-07-31T07:45:00Z
  by: human:davidjimenez75
---

# Definición

Un **bundle OKF** forma de manera natural un **grafo de conocimiento**:

- Cada archivo `.md` (concepto) es un **nodo**.
- Cada enlace markdown entre conceptos es una **arista dirigida**.
- La jerarquía de directorios añade relaciones de contención (padre-hijo).
- Los campos `sources`, `resource` y enlaces externos añaden nodos y aristas hacia el exterior.

# Propiedades útiles del grafo OKF

- **Navegable**: un agente o humano puede seguir enlaces para descubrir conocimiento relacionado.
- **Difícil**: los cambios se ven claramente en git.
- **Versionable**: cada commit es un snapshot del grafo.
- **Auto-descriptivo**: los `index.md` actúan como puntos de entrada (progressive disclosure).

# Ejemplo de recorrido

Desde el concepto [Grok](/conceptos/grok.md) se puede llegar a:

- [xAI](/conceptos/xai.md)
- [OKF](/conceptos/okf.md)
- Y desde OKF a cualquier otro concepto del bundle.

# Herramientas relacionadas

Existen plugins y herramientas que tratan OKF como grafo (análisis de impacto, visualización, detección de ciclos, etc.). Un ejemplo es el trabajo en torno a *OKF graph engineering*.

# Buenas prácticas para mantener un buen grafo

- Preferir enlaces absolutos desde la raíz del bundle (`/concepto.md`).
- Mantener los `index.md` actualizados.
- Evitar enlaces rotos (aunque OKF los tolera).
- Usar tags de forma consistente para agrupaciones transversales.
- Documentar relaciones importantes en el cuerpo del concepto (no solo el enlace).

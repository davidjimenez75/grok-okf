---
description: Skill de agente para realizar análisis de impacto sobre sistemas, contenedores, código y grafos de conocimiento (OKF) antes de aplicar cambios.
generated:
  at: 2026-07-31T08:15:00Z
  by: human:davidjimenez75
status: stable
tags:
  - skill
  - grafos
  - impacto
  - analisis
  - graph-engineering
  - riesgos
title: impact-analysis
type: Skill
verified:
  at: 2026-07-31T08:15:00Z
  by: human:davidjimenez75
---

# Por qué te lo recomiendo

Estás interesado en **ingeniería de grafos** y en mantener conocimiento estructurado. Además, en entornos Proxmox + LAMP un cambio aparentemente inocente (actualizar PHP, modificar un bridge, cambiar un esquema de BD) puede tener efectos en cascada. Este skill te ayuda a «pensar antes de actuar».

# Capacidades sugeridas

- Dado un concepto OKF, listar todos los conceptos que lo referencian (enlaces entrantes) y los que él referencia.
- Dado un cambio propuesto en un sistema (paquete, configuración, contenedor), estimar qué servicios o guests se verían afectados.
- Detectar dependencias entre contenedores LXC / Docker y servicios LAMP.
- Generar un informe de impacto legible (qué se rompe, qué hay que probar, qué hay que actualizar en el bundle).
- Sugerir el orden seguro de aplicación de un conjunto de cambios.
- Marcar conceptos como potencialmente `stale` tras un cambio importante.

# Enfoque de implementación

1. Para el grafo OKF: recorrer enlaces markdown y campos `sources` / `resource`.
2. Para infraestructura: combinar inventarios de Proxmox, contenedores y servicios systemd/Apache.
3. Mantener un pequeño grafo de dependencias (aunque sea en memoria o en un archivo auxiliar).
4. Presentar el resultado como un informe estructurado + recomendaciones de verificación.
5. Integrarse con [okf-author](okf-author.md) para proponer actualizaciones automáticas del bundle tras un cambio.

# Relación con el resto del bundle

- Se apoya directamente en [Análisis de impacto](/ingenieria-grafos/analisis-de-impacto.md) y [OKF como grafo](/ingenieria-grafos/okf-como-grafo.md).
- Es el skill de «precaución» que debería usarse antes de acciones de los otros skills de ops.

# Prioridad de implementación

**Media**. Muy valioso a medio plazo, especialmente cuando el número de conceptos y sistemas crezca.

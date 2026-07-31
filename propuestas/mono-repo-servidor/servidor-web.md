---
description: Opciones de servidor web (PHP/LAMP vs estático o propio) para publicar la documentación y el grafo OKF del monorepo.
generated:
  at: 2026-07-31T23:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - monorepo
  - servidor-web
  - php
  - lamp
  - okf
title: Servidor web para docs y OKF — Mono-repo unificado
type: Reference
verified:
  at: 2026-07-31T23:30:00Z
  by: agent:grok
---

# Objetivo del servidor web

Exponer de forma legible y navegable:

- El grafo de conceptos OKF (con visualización tipo Cytoscape, similar al `viz.html` del repo oficial de Google).
- La documentación operativa y de arquitectura.
- Búsqueda sencilla por título, tags y contenido.
- Enlaces vivos entre conceptos (los markdown links se resuelven).

No es un CMS completo; es un **visor + buscador** del monorepo.

# Opciones evaluadas

## 1. PHP / LAMP (recomendación primaria por familiaridad del usuario)

- Ventajas:
  - El usuario ya trabaja con LAMP y PHP.
  - Fácil añadir lógica dinámica (búsqueda, filtrado por tipo, autenticación básica).
  - Compatible con los stacks propuestos en pm98.dj75.net.
- Implementación mínima:
  - Un `index.php` que parsea frontmatter YAML y renderiza markdown.
  - Un endpoint `/api/graph` que devuelve el grafo en JSON para el viewer.
  - Plantillas simples (Twig o PHP puro).

## 2. Servidor estático + viewer pregenerado

- Ventajas: cero runtime, máxima seguridad y simplicidad.
- Flujo: un script (o agente) genera `viz.html` + páginas estáticas a partir del bundle OKF.
- Ideal para Caddy o Nginx sirviendo solo ficheros.

## 3. Servidor propio (Go, Rust, Node…)

- Ventajas: binario único, control total.
- Desventajas: más mantenimiento y curva de aprendizaje si no se usa ya.

# Recomendación inicial

**Empezar con PHP ligero** (porque el usuario es experto LAMP) y mantener la posibilidad de generar un export estático para entornos más restringidos.

Estructura dentro del monorepo:

```
web/
├── public/
│   ├── index.php
│   ├── assets/
│   └── viewer/          # JS del grafo (Cytoscape + marked)
├── src/
│   ├── OkfParser.php
│   ├── GraphBuilder.php
│   └── Search.php
└── templates/
```

El servidor web lee directamente los ficheros del directorio OKF (o de la raíz del monorepo), por lo que cualquier cambio en el conocimiento se refleja al instante (o tras un cache controlado).

# Seguridad básica

- Solo lectura de ficheros `.md` y assets permitidos.
- Sin ejecución de código arbitrario desde el contenido markdown.
- Autenticación opcional (Basic Auth o integración con el entorno local).
- Escuchar preferentemente en la intranet (`docs.dj75.net` o similar).

---
description: Técnica para determinar qué partes de un sistema o de un grafo de conocimiento se ven afectadas por un cambio propuesto.
generated:
  at: 2026-07-31T07:45:00Z
  by: human:davidjimenez75
status: stable
tags:
  - grafos
  - impacto
  - analisis
  - graph-engineering
  - cambios
title: Análisis de impacto
type: Reference
verified:
  at: 2026-07-31T07:45:00Z
  by: human:davidjimenez75
---

# Definición

El **análisis de impacto** (*impact analysis*) consiste en evaluar, antes de realizar un cambio, cuáles son los componentes, conceptos o sistemas que se verán afectados directa o indirectamente.

En el contexto de grafos de conocimiento (como un bundle OKF) y de sistemas de software/infraestructura, permite reducir el riesgo de regresiones y efectos colaterales no deseados.

# Aplicaciones prácticas

## En un bundle OKF

1. Identificar el concepto que se va a modificar.
2. Seguir los enlaces entrantes y salientes (y los de sus vecinos).
3. Revisar los conceptos que dependen de él (playbooks, métricas, otros references).
4. Actualizar o marcar como `stale` los documentos afectados.

## En infraestructura (Proxmox, contenedores, LAMP)

- Cambio en una plantilla LXC → impacta a todos los contenedores derivados.
- Cambio en la red de un bridge de Proxmox → afecta a todas las VMs/CT conectadas.
- Actualización de PHP o Apache → puede romper aplicaciones que dependen de extensiones o configuraciones específicas.
- Cambio de esquema en MariaDB → impacta a todas las aplicaciones y scripts que consultan esas tablas.

# Técnicas útiles

- **Grafo de dependencias**: construir (manualmente o con herramientas) el grafo de quién depende de quién.
- **Búsqueda de referencias**: `grep`, `rg` o búsquedas de código en el repositorio.
- **Tests y smoke tests**: después del cambio, verificar los caminos críticos.
- **Canary / rolling updates**: aplicar el cambio primero a un subconjunto.

# Relación con OKF

Al mantener el conocimiento en un bundle OKF bien enlazado, el análisis de impacto se vuelve más fácil: basta con seguir los enlaces del grafo de conceptos.

# Ejemplo rápido

Si se modifica el concepto [Contenedores](/sistemas/contenedores.md), hay que revisar:

- Playbooks que hablen de despliegue de contenedores.
- Documentación de Proxmox que referencie LXC/Docker.
- Cualquier métrica o procedimiento de backup relacionado.

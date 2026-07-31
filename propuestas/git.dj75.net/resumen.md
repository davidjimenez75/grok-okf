---
description: Resumen ejecutivo de la propuesta git.dj75.net — servidor Git ligero para intranet doméstica sobre Q1900M (4 GB RAM) y Debian 13.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - debian13
  - bajo-recursos
title: Resumen ejecutivo — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Objetivo

Desplegar un servidor de repositorios Git llamado **git.dj75.net** en la intranet de casa, sobre hardware muy limitado:

- Placa **ASRock Q1900M**
- CPU **Intel Celeron J1900** (4 núcleos, 2,0–2,42 GHz)
- **Solo 4 GB de RAM**
- Sistema operativo **Debian 13 (Trixie)**

El servicio debe ser estable, fácil de respaldar y suficientemente usable para uso personal / familiar / pequeños proyectos de desarrollo.

# Principios de diseño

- **Bajo consumo de memoria** como restricción dura (máximo ~1–1,5 GB para el servicio Git).
- **Simplicidad operativa**: preferir soluciones de un solo binario o paquetes oficiales de Debian.
- **Acceso principal por SSH** (el más eficiente y seguro).
- **UI web opcional** solo si cabe cómodamente.
- **Documentación viva** dentro de este bundle OKF.

# Decisión clave (recomendación)

| Prioridad | Opción recomendada              | Motivo principal                                      |
|-----------|---------------------------------|-------------------------------------------------------|
| 1ª        | Bare Git + SSH (+ Gitolite)     | Casi cero overhead, máxima fiabilidad                 |
| 2ª        | Soft Serve                      | Moderna, un solo binario, TUI + SSH, muy ligera       |
| 3ª        | Forgejo / Gitea (mínimo)        | UI web completa, viable si se recorta agresivamente    |
| Evitar    | GitLab, OneDev, GitBucket       | Consumo de RAM incompatible con 4 GB                  |

# Resultado esperado

Un servicio Git usable desde cualquier máquina de la red local (`git clone git@git.dj75.net:repo.git`), con control de acceso básico, backups sencillos y, opcionalmente, una interfaz web de solo lectura o completa según la opción elegida.

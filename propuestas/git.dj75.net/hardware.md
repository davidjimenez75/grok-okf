---
description: Características del hardware Q1900M y restricciones que condicionan las opciones de servidor Git.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - hardware
  - j1900
  - q1900m
  - bajo-recursos
title: Hardware y restricciones — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Hardware objetivo

| Componente       | Detalle                                      |
|------------------|----------------------------------------------|
| Placa base       | ASRock Q1900M                                |
| CPU              | Intel Celeron J1900 (Bay Trail, 4c/4t)       |
| Frecuencia       | 2,0 GHz base / 2,42 GHz burst                |
| RAM instalada    | **4 GB** DDR3 (límite práctico muy bajo)     |
| RAM máxima placa | Hasta 16 GB (2×8 GB) según manual ASRock     |
| Almacenamiento   | SATA (SSD recomendado)                       |
| TDP CPU          | ~10 W (muy eficiente energéticamente)        |
| Año de diseño    | ~2014                                        |

# Implicaciones para el servicio Git

- **Debian 13 mínimo** (netinst + openssh-server + git) deja aproximadamente **2,5–3 GB libres** tras arranque.
- Cualquier servicio que necesite de forma habitual **más de 1,5 GB** de RAM en reposo o bajo carga ligera es **inviable** a largo plazo.
- El J1900 es suficiente en CPU para Git (operaciones de pack/unpack no son extremadamente intensivas en repositorios de tamaño personal).
- El cuello de botella real es **siempre la RAM** y, en segundo lugar, el disco (preferir SSD).

# Recomendación de ampliación (opcional)

Si se quiere mayor holgura sin cambiar de máquina:

1. Ampliar a **8 GB** (módulo compatible DDR3-1333/1600 SO-DIMM o DIMM según el modelo exacto de placa).
2. Con 8 GB se puede ejecutar cómodamente Forgejo/Gitea + proxy + monitoring ligero.

Con los **4 GB actuales** hay que elegir opciones deliberadamente ligeras.

# Consumo energético

El sistema completo (placa + disco) suele estar en el rango de **15–25 W** en idle, lo que lo hace ideal como servidor 24/7 de bajo coste eléctrico.

---
description: Estimación de consumo de recursos de las distintas opciones de servidor Git sobre el hardware Q1900M con 4 GB RAM.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - recursos
  - dimensionamiento
  - ram
title: Estimación de recursos — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Contexto de hardware

- CPU: Intel Celeron J1900 (4 núcleos)
- RAM total: **4 GB**
- Debian 13 mínimo + openssh + git ≈ **0,8–1,2 GB** en uso tras arranque
- Memoria disponible real para el servicio Git ≈ **2,5–3 GB**

# Estimación por opción (reposo + carga ligera)

| Opción                     | RAM en reposo | RAM bajo push/clone | CPU | Disco base | Notas                                      |
|----------------------------|---------------|---------------------|-----|------------|--------------------------------------------|
| Bare Git + SSH             | < 30 MB       | picos cortos        | Baja| ~50 MB     | Casi negligibles                           |
| Gitolite                   | 40–80 MB      | picos cortos        | Baja| ~100 MB    | Perl + git                                 |
| Soft Serve                 | 20–60 MB      | 80–150 MB           | Baja| ~30 MB     | Binario Go muy eficiente                   |
| Forgejo/Gitea (SQLite min) | 150–350 MB    | 400–700 MB          | Media| ~150 MB   | Depende de nº de repos y features activas  |
| + nginx/Caddy              | +20–40 MB     | —                   | Baja| —          | Solo si se necesita UI web                 |
| + cgit/gitweb              | +15–30 MB     | —                   | Baja| —          | Solo lectura                               |

# Márgenes de seguridad recomendados

- Dejar siempre **al menos 500–800 MB libres** para el kernel, caché de página y picos inesperados.
- Monitorizar con `htop`, `free -h` y, si se desea, un exporter ligero de Prometheus o solo `vnstat` + logs.

# Almacenamiento de repositorios

- Los repositorios bare ocupan aproximadamente el mismo espacio que el working tree (a veces menos gracias a la compresión).
- Prever crecimiento: 50–200 GB suele ser más que suficiente para uso personal/familiar durante años.
- Preferir **SSD SATA** frente a HDD mecánico por la latencia de las operaciones de pack.

# Escalado futuro

1. Ampliar RAM a **8 GB** → se puede ejecutar Forgejo cómodamente + otros servicios ligeros.
2. Mover el servicio a un CT dentro de un host Proxmox más potente (ver propuesta pm98.dj75.net).
3. Mantener este nodo como mirror de solo lectura o backup offline.

# Conclusión de dimensionamiento

Con **4 GB** las opciones 1–3 (Bare, Gitolite, Soft Serve) son las únicas que dejan un margen de seguridad cómodo. Forgejo es viable solo con configuración muy recortada y vigilancia del uso de memoria.

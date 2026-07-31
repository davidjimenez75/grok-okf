---
description: Número de usuarios únicos que interactúan con un servicio o sistema en un periodo de tiempo definido.
generated:
  at: 2026-07-31T07:55:00Z
  by: human:davidjimenez75
status: stable
tags:
  - metrica
  - usuarios
  - monitorizacion
title: Usuarios activos
type: Metric
verified:
  at: 2026-07-31T07:55:00Z
  by: human:davidjimenez75
---

# Definición

**Usuarios activos** mide cuántas personas distintas han interactuado con un servicio durante un periodo concreto (diario, semanal, mensual).

Es una métrica fundamental de adopción y salud de un producto o servicio.

# Variantes comunes

- **DAU** (Daily Active Users)
- **WAU** (Weekly Active Users)
- **MAU** (Monthly Active Users)
- **Usuarios concurrentes** (pico en un momento dado)

# Cómo se suele calcular

Depende del sistema:

- Logs de acceso (Apache/Nginx, autenticación).
- Eventos de aplicación (login, acciones significativas).
- Contadores en base de datos o sistemas de analítica.

Ejemplo conceptual con SQL (MariaDB):

```sql
SELECT COUNT(DISTINCT user_id) AS dau
FROM access_logs
WHERE event_time >= CURDATE()
  AND event_time < CURDATE() + INTERVAL 1 DAY;
```

# Consideraciones

- Definir claramente qué cuenta como «activo» (solo login, o una acción significativa).
- Evitar contar bots y scrapers.
- Tener en cuenta usuarios anónimos vs autenticados.
- La métrica por sí sola no indica calidad de uso (hay que combinarla con engagement).

# Relación con este bundle

Esta métrica se incluye como ejemplo de concepto de tipo `Metric` dentro de un bundle OKF. En un entorno real se complementaría con un `Attested Computation` que definiera exactamente cómo se calcula.

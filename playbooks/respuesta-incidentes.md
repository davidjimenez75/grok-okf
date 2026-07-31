---
description: Procedimiento estructurado para detectar, triar, mitigar y documentar incidentes de servicio.
generated:
  at: 2026-07-31T07:50:00Z
  by: human:davidjimenez75
status: stable
tags:
  - playbook
  - incidentes
  - operaciones
  - oncall
title: Respuesta a incidentes
type: Playbook
verified:
  at: 2026-07-31T07:50:00Z
  by: human:davidjimenez75
---

# Objetivo

Restaurar el servicio lo más rápido posible minimizando el impacto, documentando todo el proceso y evitando que el incidente se repita.

# Fases

## 1. Detección y alerta

- Recibir alerta (monitorización, usuario, log).
- Confirmar que es real (no falso positivo).
- Registrar hora de detección.

## 2. Triaje (prioridad)

| Severidad | Criterio                              | Tiempo de respuesta objetivo |
|-----------|---------------------------------------|------------------------------|
| Crítica   | Servicio completamente caído          | Inmediato                    |
| Alta      | Degradación grave / datos en riesgo   | < 15 min                     |
| Media     | Funcionalidad parcial afectada        | < 1 h                        |
| Baja      | Problema menor / cosmético            | < 24 h                       |

## 3. Mitigación inmediata

1. Aislar el problema (reiniciar servicio, failover, deshabilitar feature).
2. Comunicar estado (canal de incidentes, status page si existe).
3. Evitar cambios no necesarios mientras se investiga.

## 4. Diagnóstico

- Revisar logs recientes (`journalctl`, logs de Apache/PHP, Proxmox, contenedores).
- Comprobar recursos (CPU, RAM, disco, red).
- Verificar cambios recientes (deploys, actualizaciones, configuraciones).

## 5. Resolución y verificación

- Aplicar la corrección.
- Verificar que el servicio vuelve a la normalidad.
- Monitorizar durante un periodo de observación.

## 6. Post-mortem (obligatorio en Crítica/Alta)

Documentar:

- Timeline completo.
- Causa raíz.
- Acciones correctivas y preventivas.
- Lecciones aprendidas.

# Plantilla rápida de actualización de estado

```
[INCIDENTE] Severidad: Alta
Estado: Investigando / Mitigando / Resuelto
Impacto: ...
Acciones en curso: ...
Próxima actualización: en X minutos
```

# Referencias relacionadas

- [Proxmox VE](/sistemas/proxmox.md)
- [Contenedores](/sistemas/contenedores.md)
- [LAMP](/desarrollo/lamp.md)

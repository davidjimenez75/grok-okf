---
description: Configuración de red y DNS para el FQDN grok.dj75.net.
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - red
  - dns
  - fqdn
title: Red y DNS — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# FQDN

- **Nombre canónico**: `grok.dj75.net`
- Zona DNS: `dj75.net` (interna o pública según el diseño de la red doméstica/servidor).

# Resolución

| Entorno          | Resolución recomendada                          |
|------------------|-------------------------------------------------|
| Red local        | Registro A (o CNAME) apuntando a la IP del CT o del proxy |
| Acceso externo   | Si se expone: registro A + proxy con TLS        |
| Interno (Proxmox)| Puede usarse también el hostname corto `grok`   |

# Puertos

| Servicio     | Puerto interno CT | Exposición                          |
|--------------|-------------------|-------------------------------------|
| ttyd         | 7681              | Solo vía proxy HTTPS (443)          |
| SSH          | 22 (o alternativo)| Solo red interna o con restricciones|
| Agente (API) | opcional          | No exponer públicamente             |

# Proxy inverso

El tráfico HTTPS hacia `grok.dj75.net` se termina en el CT proxy existente (el mismo que se usa para otros servicios de pm98.dj75.net) y se reenvía al CT del agente.

# IPv6

Si la red lo soporta, añadir registro AAAA correspondiente. El resto de la configuración (proxy, ttyd) debe ser dual-stack.

# Notas

- Preferir IP estática o reserva DHCP para el CT.
- Documentar la IP y el hostname en el inventario de red del bundle OKF.

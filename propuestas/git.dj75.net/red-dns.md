---
description: Configuración de red y resolución DNS para el servicio git.dj75.net en la intranet doméstica.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - red
  - dns
  - intranet
title: Red y DNS — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Alcance

El servicio está pensado principalmente para la **intranet doméstica**. No es obligatorio (ni recomendable con 4 GB) exponerlo a Internet sin medidas adicionales.

# Resolución de nombres

Opciones (de más simple a más elaborada):

1. **Entrada estática en el router** (DHCP reservation + DNS local del router)  
   `git.dj75.net` → IP fija del Q1900M.

2. **Servidor DNS interno** (dnsmasq, Unbound, AdGuard Home, Pi-hole…)  
   Zona o registro A para `git.dj75.net` y, si se usa, `*.git.dj75.net`.

3. **Archivo /etc/hosts** en las máquinas cliente (solo para pruebas o entornos muy pequeños).

# Puertos

| Servicio              | Puerto | Protocolo | Notas                                      |
|-----------------------|--------|-----------|--------------------------------------------|
| SSH (Git)             | 22     | TCP       | Principal. Cambiar a 2222 si se prefiere   |
| Soft Serve SSH        | 23231  | TCP       | Por defecto de Soft Serve (configurable)   |
| Forgejo HTTP          | 3000   | TCP       | Solo localhost + proxy                     |
| Proxy HTTP/HTTPS      | 80/443 | TCP       | Solo si se activa UI web                   |
| cgit / gitweb         | 80     | TCP       | Solo lectura, idealmente solo LAN          |

# Firewall (ufw / nftables)

Política recomendada en el host:

```bash
# Ejemplo ufw
ufw default deny incoming
ufw default allow outgoing
ufw allow from 192.168.0.0/16 to any port 22 proto tcp   # o la subred real
ufw allow from 192.168.0.0/16 to any port 80 proto tcp   # si hay web
ufw enable
```

Restringir siempre el origen a la LAN. No abrir SSH ni web a `0.0.0.0/0` sin VPN o fail2ban + claves únicamente.

# Acceso desde fuera de casa (opcional)

- **WireGuard / Tailscale / Netbird** (preferido): el cliente se conecta a la VPN y resuelve `git.dj75.net` normalmente.
- Reverse proxy + autenticación fuerte (menos recomendable con hardware tan limitado).

# Certificados TLS

- Para uso solo LAN: certificado autofirmado o CA interna (step-ca, smallstep, etc.).
- Si se expone: Let’s Encrypt vía DNS challenge o HTTP challenge a través de un proxy que sí tenga IP pública.

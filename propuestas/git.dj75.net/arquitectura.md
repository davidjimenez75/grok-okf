---
description: Arquitectura lógica recomendada para git.dj75.net según la opción elegida.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - arquitectura
  - git
  - ssh
title: Arquitectura — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Vista general (opción recomendada: Bare Git + SSH o Soft Serve)

```
git.dj75.net (Debian 13 bare-metal o LXC)
│
├── Sistema base mínimo
│   ├── openssh-server
│   ├── git
│   └── usuario del sistema: git (o softserve)
│
├── Almacenamiento de repositorios
│   └── /var/lib/git/repositories/   (o /home/git/repos/)
│
├── Autenticación
│   └── ~/.ssh/authorized_keys  (o gestión interna de Soft Serve / Gitolite)
│
└── (Opcional) Capa web de solo lectura
    ├── cgit o gitweb
    └── nginx / lighttpd / Caddy (puerto 80/443 solo LAN)
```

# Variante con Forgejo / Gitea

```
git.dj75.net
│
├── Forgejo / Gitea (binario o paquete)
│   ├── SQLite
│   ├── datos en /var/lib/forgejo/
│   └── escucha en 127.0.0.1:3000
│
├── Proxy inverso ligero (Caddy o nginx)
│   └── termina TLS (si se expone fuera de LAN) o solo HTTP interno
│
└── SSH nativo de Forgejo (puerto 2222 o 22)
```

# Decisiones de diseño comunes

- **Un solo servicio principal**: evitar apilar demasiados daemons.
- **Datos en disco local**: preferiblemente SSD. Los repos Git son sensibles a la latencia de escritura en operaciones de push grandes.
- **Sin contenedores anidados** si se ejecuta bare-metal: simplifica el consumo de memoria.
- Si el host es un **LXC dentro de Proxmox** (ver propuesta pm98.dj75.net): asignar 1,5–2 GB de RAM al CT y dejar el resto al host.

# Flujo de uso típico

1. El desarrollador configura la clave SSH en el servidor (o la registra en Soft Serve / Gitolite / Forgejo).
2. `git clone git@git.dj75.net:proyecto.git`
3. Trabajo local + `git push` / `git pull`.
4. (Opcional) Navegación web de commits vía cgit o la UI de Forgejo.

# Relación con otras propuestas

En la propuesta **pm98.dj75.net** ya se contempla un CT `ct-git` (Forgejo/Gitea). **git.dj75.net** es la alternativa de **bajo coste energético y bajo hardware** para cuando no se dispone del servidor potente o se quiere un nodo dedicado y siempre encendido con consumo mínimo.

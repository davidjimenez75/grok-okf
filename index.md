---
okf_version: "0.2"
---

# Bundle de conocimiento Grok-OKF

Conocimiento práctico sobre Grok, xAI, OKF, sistemas, desarrollo, grafos de conocimiento, skills de agente y propuestas de implementación, redactado en español de España.

# Conceptos

* [Grok](conceptos/grok.md) - Modelo de lenguaje de xAI orientado a la búsqueda de la verdad
* [OKF](conceptos/okf.md) - Open Knowledge Format: formato abierto de conocimiento
* [xAI](conceptos/xai.md) - Empresa de inteligencia artificial fundada por Elon Musk

# Sistemas e infraestructura

* [Proxmox VE](sistemas/proxmox.md) - Plataforma de virtualización open-source con KVM y LXC
* [Contenedores](sistemas/contenedores.md) - Docker, Podman y LXC: diferencias y buenas prácticas
* [Debian](sistemas/debian.md) - Sistema operativo base estable para servidores y Proxmox

# Desarrollo y programación

* [PHP](desarrollo/php.md) - Lenguaje de programación del lado del servidor
* [LAMP](desarrollo/lamp.md) - Stack Linux + Apache + MySQL/MariaDB + PHP
* [Git](desarrollo/git.md) - Control de versiones distribuido

# Ingeniería de grafos

* [OKF como grafo](ingenieria-grafos/okf-como-grafo.md) - Cómo un bundle OKF forma un grafo de conocimiento
* [Análisis de impacto](ingenieria-grafos/analisis-de-impacto.md) - Evaluar el alcance de cambios en sistemas interdependientes

# Skills recomendados

* [proxmox-ops](skills/proxmox-ops.md) - Operaciones y gestión de Proxmox VE
* [container-ops](skills/container-ops.md) - Gestión de contenedores (LXC, Docker, Podman)
* [lamp-ops](skills/lamp-ops.md) - Operaciones del stack LAMP
* [okf-author](skills/okf-author.md) - Creación y mantenimiento de bundles OKF
* [debian-sysadmin](skills/debian-sysadmin.md) - Administración de sistemas Debian
* [impact-analysis](skills/impact-analysis.md) - Análisis de impacto en sistemas y grafos

# Propuestas

* [pm98.dj75.net](propuestas/pm98.dj75.net/) - Servidor Proxmox VE 9.2 con contenedores Debian 13 para .NET 10, SQL Server, Rust, LAMP y PrestaShop
* [git.dj75.net](propuestas/git.dj75.net/) - Servidor Git ligero para intranet doméstica sobre Debian 13 y hardware Q1900M (4 GB RAM)
* [mono-repo-servidor](propuestas/mono-repo-servidor/) - Monorepo unificado de operaciones de servidor + conocimiento OKF + documentación + servidor web + agentes autónomos

# Métricas

* [Usuarios activos](metricas/usuarios-activos.md) - Número de usuarios que interactúan con un servicio en un periodo determinado

# Playbooks

* [Respuesta a incidentes](playbooks/respuesta-incidentes.md) - Procedimiento para gestionar incidentes de servicio
* [Backup y restauración en Proxmox](playbooks/backup-proxmox.md) - Cómo hacer y restaurar backups de VMs y contenedores

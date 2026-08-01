# Registro de actualizaciones del bundle

## 2026-08-01

* **Nueva propuesta grok.dj75.net**: Contenedor LXC Debian 13 dedicado a un agente autónomo potenciado por Grok, con FQDN `grok.dj75.net` e interfaz web de terminal/SSH (ttyd) que permite interactuar directamente con Grok desde el navegador.
  - Documentos: resumen, arquitectura, contenedor, agente-autonomo, interfaz-web-terminal, red-dns, seguridad-backups, plan-implementacion, recursos.
  - Integración con la visión de agentes del mono-repo y con el resto de la infraestructura Proxmox/Debian 13.

## 2026-07-31

* **Nueva propuesta mono-repo-servidor**: Monorepo unificado que concentra:
  - Scripts de instalación, verificación y actualización
  - Comandos CLI (preferencia `/usr/local/bin`)
  - Documentación y conocimiento OKF (tareas, ideas, mapas mentales, diagramas, infraestructura)
  - Servidor web (PHP/LAMP o estático) para docs y grafo OKF
  - Mantenimiento autónomo con Grok Build, Claude Code, OpenCode y Codex
  - Documentos: resumen, arquitectura, estructura-repo, scripts-comandos, servidor-web, agentes-autonomos, plan-implementacion, opciones-binarios
* **Propuesta git.dj75.net ampliada**: Añadidos ficheros individuales detallados para cada opción de software:
  - `opciones/bare-git-ssh.md`
  - `opciones/gitolite.md`
  - `opciones/soft-serve.md`
  - `opciones/forgejo.md`
  - `opciones/gitlab.md`
  - Actualizada la comparativa general con escenarios de 4 / 8 / 16 GB de RAM.
* **Nueva propuesta git.dj75.net**: Servidor Git ligero para intranet doméstica sobre Debian 13 y hardware ASRock Q1900M (Intel Celeron J1900 + 4 GB RAM).
  - Documentos: resumen, hardware, opciones de software (Bare Git, Gitolite, Soft Serve, Forgejo/Gitea), arquitectura, red/DNS, seguridad y backups, plan de implementación y recursos.
  - Enfoque en bajo consumo de memoria y varias alternativas viables.
* **Nueva sección Propuestas**: Añadida propuesta completa de implementación del servidor **pm98.dj75.net**:
  - Resumen, arquitectura, host Proxmox VE 9.2, contenedores Debian 13
  - Red/DNS, seguridad y backups, plan de implementación, recursos
  - Stacks detallados: .NET 10, SQL Server, Rust, PHP/LAMP, PrestaShop
* **Nueva sección Skills**: 6 skills de agente recomendados (proxmox-ops, container-ops, lamp-ops, okf-author, debian-sysadmin, impact-analysis).
* **Ampliación mayor**: Secciones de sistemas, desarrollo, ingeniería de grafos, playbooks y métricas.
* **Convención**: Frontmatter ordenado alfabéticamente. Contenidos en español de España.

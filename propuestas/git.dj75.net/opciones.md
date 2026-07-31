---
description: Comparativa de opciones de software para alojar repositorios Git en git.dj75.net según la RAM disponible.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - gitea
  - forgejo
  - soft-serve
  - gitolite
  - gitlab
title: Opciones de software — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
---

# Tabla comparativa rápida

| Opción                  | RAM aprox. (idle) | UI web          | Control acceso     | Compatible 4 GB | Compatible 8 GB | Compatible 16 GB |
|-------------------------|-------------------|-----------------|--------------------|-----------------|-----------------|------------------|
| Bare Git + SSH          | < 50 MB           | No (opcional cgit) | authorized_keys | **Sí (ideal)**  | Sí              | Sí               |
| Gitolite                | < 80 MB           | No              | Excelente (ACL)    | **Sí**          | Sí              | Sí               |
| Soft Serve              | 20–60 MB          | TUI + SSH       | Claves + collabs   | **Sí**          | Sí              | Sí               |
| Forgejo / Gitea         | 150–400 MB        | Completa        | Usuarios/orgs      | Condicional     | **Sí (recomendado)** | Sí          |
| GitLab CE               | varios GB         | Completa + CI   | Completo           | **No**          | Justo (ajustes) | **Razonable**    |

# Ficheros detallados

* [Bare Git + SSH](opciones/bare-git-ssh.md)
* [Gitolite](opciones/gitolite.md)
* [Soft Serve](opciones/soft-serve.md)
* [Forgejo / Gitea](opciones/forgejo.md)
* [GitLab CE](opciones/gitlab.md)

# Resumen por escenario de RAM

## Con 4 GB (configuración actual)

Opciones recomendadas, de más simple a más completa:

1. **Bare Git + SSH** — máxima robustez y mínimo consumo.
2. **Gitolite** — si se necesitan permisos finos entre varios usuarios.
3. **Soft Serve** — si se quiere una experiencia moderna con TUI.
4. **Forgejo** solo si la UI web es imprescindible y se acepta recortar funcionalidades.

GitLab **no** es viable.

## Con 8 GB

- **Forgejo / Gitea** pasa a ser la opción más equilibrada (UI web completa y holgada).
- Soft Serve / Gitolite / Bare siguen siendo excelentes si no se necesita web.
- GitLab CE es posible solo con muchos ajustes y rendimiento limitado por el CPU J1900.

## Con 16 GB

- **Forgejo** sigue siendo la recomendación principal por fluidez.
- **GitLab CE** se vuelve usable para uso personal, aunque el procesador J1900 seguirá notándose en operaciones pesadas y CI.

# Opciones descartadas o menos recomendables

- **Gogs**: menos activo; Forgejo/Gitea lo superan.
- **OneDev / GitBucket**: basados en Java → mayor consumo de RAM.
- **GitLab** en 4 GB: inviable.

# Recomendación final

| Prioridad | Situación                              | Opción recomendada      |
|-----------|----------------------------------------|-------------------------|
| 1         | 4 GB + uso CLI                         | Bare Git o Soft Serve   |
| 2         | 4 GB + varios usuarios con permisos    | Gitolite                |
| 3         | 8 GB + se quiere UI web                | **Forgejo**             |
| 4         | 16 GB + se necesita CI/CD de GitLab    | GitLab CE (con reservas por CPU) |

---
description: Sistema de control de versiones distribuido, estándar de facto para el desarrollo de software colaborativo y personal.
generated:
  at: 2026-07-31T07:40:00Z
  by: human:davidjimenez75
status: stable
tags:
  - git
  - control-de-versiones
  - desarrollo
  - github
title: Git
type: Reference
verified:
  at: 2026-07-31T07:40:00Z
  by: human:davidjimenez75
---

# Definición

**Git** es un sistema de control de versiones distribuido creado por Linus Torvalds. Permite gestionar el historial de cambios de un proyecto de forma eficiente, con soporte nativo para ramas, merges y trabajo offline.

# Comandos esenciales

```bash
# Inicializar y clonar
git init
git clone <url>

# Estado y cambios
git status
git add .
git commit -m "mensaje claro y conciso"
git push
git pull

# Ramas
git branch
git checkout -b feature/nueva-funcionalidad
git merge main
git branch -d feature/nueva-funcionalidad

# Historial
git log --oneline --graph --all
git show <commit>

# Deshacer
git restore <archivo>          # descartar cambios no staged
git reset --soft HEAD~1        # deshacer último commit manteniendo cambios
```

# Flujos de trabajo recomendados

- **main/master** siempre estable y desplegable.
- Trabajar en ramas cortas (`feature/`, `fix/`, `hotfix/`).
- Hacer commits atómicos y con mensajes descriptivos.
- Usar Pull Requests / Merge Requests para revisión.
- Preferir `rebase` para historial lineal en ramas de feature (con cuidado).

# Configuración útil

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --global init.defaultBranch main
git config --global pull.rebase false   # o true según preferencia
git config --global core.editor "nano"  # o vim, code...
```

# Buenas prácticas

- Nunca hacer `force push` a ramas compartidas (`main`).
- Usar `.gitignore` adecuadamente (no subir secretos, vendor, node_modules…).
- Firmar commits cuando sea posible (`git commit -S`).
- Mantener el historial limpio y legible.

# Enlaces útiles

- Documentación oficial: https://git-scm.com/doc
- Pro Git book (gratis): https://git-scm.com/book/es/v2
- GitHub Docs: https://docs.github.com/

---
description: Capa de control de acceso fino (ACL) sobre repositorios Git bare mediante Gitolite.
generated:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - gitolite
  - acl
  - bajo-recursos
title: Gitolite — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
---

# Resumen

Gitolite es una capa de autorización que se sitúa encima de Git. Utiliza un único usuario Unix (`git`) y gestiona muchos “usuarios lógicos” identificados por sus claves SSH. La configuración de permisos se hace editando y haciendo push al repositorio especial `gitolite-admin`.

# Requisitos de recursos (Q1900M)

| Recurso     | Uso aproximado      |
|-------------|---------------------|
| RAM         | < 80 MB             |
| CPU         | Muy bajo            |
| Disco base  | ~100 MB + repos     |
| Compatible con 4 GB | **Sí**         |

# Características principales

- Control de acceso a nivel de repositorio, rama, etiqueta e incluso ficheros/directorios.
- Grupos de usuarios y de repositorios.
- Creación de repositorios “wild” (bajo demanda) si se habilita.
- Sin interfaz web (se puede combinar con cgit/gitweb).
- Muy maduro (usado por kernel.org, Fedora, Gentoo, KDE, etc.).

# Instalación orientativa (Debian 13)

```bash
apt update
apt install -y git openssh-server perl

# Crear usuario git
adduser --system --group --home /var/lib/git --shell /bin/bash git

# Como administrador, generar o usar una clave SSH y seguir la guía oficial:
# https://gitolite.com/gitolite/install.html

# Resumen típico (desde la máquina de administración):
su - git
git clone https://github.com/sitaramc/gitolite
gitolite/install -ln
gitolite setup -pk /ruta/a/tu-clave-admin.pub
```

Después se clona `git@servidor:gitolite-admin`, se edita `conf/gitolite.conf` y se hace push.

# Ejemplo de configuración

```conf
repo gitolite-admin
    RW+     =  admin

repo testing
    RW+     =  david
    R       =  familia

@devs = david ana

repo proyecto-secreto
    RW+     =  @devs
    -       =  @all
```

# Ventajas

- ACL muy granulares.
- Extremadamente ligero.
- Un solo usuario Unix → menos superficie de ataque.
- Configuración versionada en Git.

# Desventajas

- Curva de aprendizaje de la sintaxis de `gitolite.conf`.
- Documentación densa.
- Sin UI web nativa.

# Cuándo elegirla

- Varios usuarios con permisos distintos.
- Se necesita control fino (ramas protegidas, etc.).
- Se quiere mantener el consumo de RAM mínimo en el Q1900M.

# Relación con otros documentos

- [Comparativa general](../opciones.md)
- [Bare Git + SSH](bare-git-ssh.md) (base sobre la que se asienta)
- [Seguridad y backups](../seguridad-backups.md)

---
description: Opción mínima de servidor Git basada en repositorios bare y acceso exclusivo por SSH.
generated:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - ssh
  - bare
  - bajo-recursos
title: Bare Git + SSH — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
---

# Resumen

La opción más ligera y robusta. Solo se usan los paquetes oficiales `git` y `openssh-server`. Los repositorios se crean como bare y se sirven exclusivamente por SSH.

# Requisitos de recursos (Q1900M)

| Recurso     | Uso aproximado      |
|-------------|---------------------|
| RAM         | < 50 MB             |
| CPU         | Mínimo              |
| Disco base  | ~50 MB + tamaño repos |
| Compatible con 4 GB | **Sí (ideal)** |

# Componentes

- `openssh-server`
- `git`
- Usuario de sistema `git` (sin shell interactivo completo, preferible `git-shell`)
- Directorio de repositorios, por ejemplo `/var/lib/git/repositories/`

# Instalación orientativa (Debian 13)

```bash
apt update
apt install -y openssh-server git

adduser --system --group --home /var/lib/git --shell /usr/bin/git-shell git
mkdir -p /var/lib/git/repositories /var/lib/git/.ssh
chmod 700 /var/lib/git/.ssh
chown -R git:git /var/lib/git

# Añadir claves públicas autorizadas
nano /var/lib/git/.ssh/authorized_keys
chmod 600 /var/lib/git/.ssh/authorized_keys
chown git:git /var/lib/git/.ssh/authorized_keys
```

Crear un repositorio:

```bash
sudo -u git git init --bare /var/lib/git/repositories/mi-proyecto.git
```

Uso desde el cliente:

```bash
git clone git@git.dj75.net:mi-proyecto.git
# o con ruta completa si no se configura el home correctamente:
# git clone git@git.dj75.net:/var/lib/git/repositories/mi-proyecto.git
```

# Ampliaciones opcionales y ligeras

- **cgit** o **gitweb** + nginx/lighttpd para navegación web de solo lectura.
- Script simple de creación de repos (`newrepo.sh`).
- Restricción de comandos en `authorized_keys` con `command="..."`.

# Ventajas

- Consumo de recursos casi nulo.
- Máxima fiabilidad y compatibilidad.
- Backups triviales (copiar el directorio de repos).
- Sin dependencias de bases de datos ni servicios extra.

# Desventajas

- Sin interfaz web nativa.
- Gestión de permisos manual (o mediante scripts / Gitolite).

# Cuándo elegirla

- Uso personal o familiar muy reducido.
- Se trabaja principalmente desde terminal o clientes Git (VS Code, etc.).
- Se prioriza estabilidad absoluta y mínimo consumo en el Q1900M con 4 GB.

# Relación con otros documentos

- [Comparativa general](../opciones.md)
- [Arquitectura](../arquitectura.md)
- [Seguridad y backups](../seguridad-backups.md)

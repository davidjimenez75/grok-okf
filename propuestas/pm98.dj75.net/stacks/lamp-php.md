---
description: Configuración de contenedores Debian 13 con el stack LAMP (Apache + PHP + MariaDB) para desarrollo.
generated:
  at: 2026-07-31T08:45:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - lamp
  - php
  - apache
  - mariadb
  - stack
title: Stack PHP / LAMP — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:45:00Z
  by: human:davidjimenez75
---

# Componentes

- **Apache 2.4**
- **PHP 8.4** (o 8.3 según necesidad del proyecto)
- **MariaDB** (versión estable de Debian 13)
- Composer 2.x

# Contenedor recomendado

- Base: plantilla `debian13-lamp`
- Recursos orientativos: 2 vCPU, 2-4 GB RAM, 30 GB disco

# Instalación típica (Debian 13)

```bash
apt update
apt install -y apache2 mariadb-server \
  php php-mysql php-xml php-mbstring php-curl \
  php-zip php-gd php-intl php-opcache \
  libapache2-mod-php composer

a2enmod rewrite headers ssl
systemctl restart apache2
```

# Virtual hosts

- Un virtual host por proyecto o por CT.
- DocumentRoot bajo `/var/www/<proyecto>`.
- `AllowOverride All` para soportar `.htaccess`.

# Buenas prácticas

- `display_errors = Off` en producción-like; logs en archivo.
- OPcache habilitado.
- Bases de datos con usuarios específicos por aplicación (principio de mínimo privilegio).
- Backups de las bases de datos además del backup del CT completo.

# Relación con otros documentos

- [LAMP](/desarrollo/lamp.md)
- [PHP](/desarrollo/php.md)
- Skill: [lamp-ops](/skills/lamp-ops.md)

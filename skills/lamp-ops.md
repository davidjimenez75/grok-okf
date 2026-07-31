---
description: Skill de agente para operar el stack LAMP (Apache, PHP, MariaDB/MySQL) de forma segura y reproducible.
generated:
  at: 2026-07-31T08:10:00Z
  by: human:davidjimenez75
status: stable
tags:
  - skill
  - lamp
  - php
  - apache
  - mariadb
  - web
title: lamp-ops
type: Skill
verified:
  at: 2026-07-31T08:10:00Z
  by: human:davidjimenez75
---

# Por qué te lo recomiendo

Tu bio lleva el hashtag **#lamp #php**. El stack LAMP sigue siendo el núcleo de muchos de tus proyectos. Un skill dedicado permite al agente ayudar en deploys, diagnóstico, backups de bases de datos y configuración de virtual hosts sin que tengas que recordar cada detalle de `a2ensite` o `mysqldump`.

# Capacidades sugeridas

- Listar virtual hosts de Apache y su estado (enabled/disabled).
- Crear / habilitar / deshabilitar virtual hosts a partir de plantillas.
- Gestionar módulos de Apache (`a2enmod` / `a2dismod`).
- Ejecutar y verificar configuración de PHP (`php -i`, OPcache, versiones).
- Hacer dumps y restauraciones de bases de datos MariaDB/MySQL.
- Comprobar logs de error de Apache y PHP de forma inteligente (filtrado por fecha/severity).
- Desplegar una aplicación PHP simple (composer install, permisos, clear cache).
- Verificar certificados SSL y renovación con certbot.

# Enfoque de implementación

1. Operar preferentemente **dentro de un contenedor LXC** (aislado) en lugar de en el host Proxmox.
2. Usar comandos estándar de Debian (`apache2ctl`, `mysql`, `php`) y plantillas de configuración versionadas.
3. Nunca almacenar contraseñas de base de datos en el skill; usar variables de entorno o un vault.
4. Confirmación humana para cambios en producción (nuevos vhosts, cambios de schema, etc.).

# Relación con el resto del bundle

- Se apoya en [LAMP](/desarrollo/lamp.md), [PHP](/desarrollo/php.md) y [Debian](/sistemas/debian.md).
- Combina bien con [container-ops](container-ops.md) cuando el LAMP vive dentro de un LXC.

# Prioridad de implementación

**Alta-Media**. Muy útil si mantienes varios sitios o aplicaciones PHP.

---
description: Stack de software clásico y robusto formado por Linux, Apache, MySQL/MariaDB y PHP para el desarrollo y despliegue de aplicaciones web.
generated:
  at: 2026-07-31T07:40:00Z
  by: human:davidjimenez75
status: stable
tags:
  - lamp
  - apache
  - mysql
  - mariadb
  - php
  - web
title: LAMP
type: Reference
verified:
  at: 2026-07-31T07:40:00Z
  by: human:davidjimenez75
---

# Definición

**LAMP** es el acrónimo de **L**inux + **A**pache + **M**ySQL/MariaDB + **P**HP. Es uno de los stacks más maduros, estables y ampliamente usados para aplicaciones web dinámicas.

Aunque existen alternativas modernas (LEMP con Nginx, stacks con Node, etc.), LAMP sigue siendo excelente para la mayoría de proyectos tradicionales y CMS.

# Componentes

| Componente     | Rol                                      | Alternativas comunes      |
|----------------|------------------------------------------|---------------------------|
| Linux          | Sistema operativo (Debian, Ubuntu…)     | -                         |
| Apache         | Servidor web                             | Nginx, Caddy              |
| MySQL/MariaDB  | Base de datos relacional                 | PostgreSQL, SQLite        |
| PHP            | Lenguaje de programación del lado servidor | -                       |

# Instalación rápida en Debian 12

```bash
apt update
apt install apache2 mariadb-server php php-mysql libapache2-mod-php

# Asegurar MariaDB
mysql_secure_installation

# Habilitar módulos útiles
a2enmod rewrite headers ssl
systemctl restart apache2
```

# Virtual hosts recomendados

Usar archivos en `/etc/apache2/sites-available/` y habilitar con `a2ensite`.

Ejemplo mínimo:

```apache
<VirtualHost *:80>
    ServerName ejemplo.local
    DocumentRoot /var/www/ejemplo

    <Directory /var/www/ejemplo>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/ejemplo-error.log
    CustomLog ${APACHE_LOG_DIR}/ejemplo-access.log combined
</VirtualHost>
```

# Buenas prácticas

- Separar código, configuración y datos.
- Usar HTTPS siempre (Let's Encrypt + certbot).
- Configurar `open_basedir` y desactivar funciones peligrosas en `php.ini`.
- Hacer backups regulares de la base de datos (`mysqldump` o `mariadb-dump`).
- Monitorizar logs de Apache y PHP.
- En Proxmox: instalar LAMP dentro de un contenedor LXC Debian para aislamiento.

# Enlaces útiles

- Apache: https://httpd.apache.org/docs/
- MariaDB: https://mariadb.com/kb/en/documentation/
- PHP: https://www.php.net/

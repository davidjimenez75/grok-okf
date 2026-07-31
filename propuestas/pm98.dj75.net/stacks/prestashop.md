---
description: Configuración recomendada de contenedores para PrestaShop 9.x sobre Debian 13 + LAMP.
generated:
  at: 2026-07-31T08:45:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - prestashop
  - ecommerce
  - php
  - stack
title: Stack PrestaShop — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:45:00Z
  by: human:davidjimenez75
---

# Versión objetivo

- **PrestaShop 9.x**
- PHP recomendado: **8.3 o 8.4** (8.5 también contemplado en documentación reciente)
- MariaDB / MySQL reciente

# Contenedor recomendado

- Base: plantilla `debian13-lamp` o `debian13-prestashop`
- Recursos orientativos: 2-4 vCPU, 4-6 GB RAM, 40-60 GB disco
- Un CT por tienda cuando sea posible (mejor aislamiento)

# Requisitos principales

- PHP con extensiones: `curl`, `gd`, `intl`, `mbstring`, `openssl`, `pdo_mysql`, `zip`, etc.
- `memory_limit` ≥ 256M (recomendado 512M)
- `max_execution_time` generoso
- `mod_rewrite` habilitado
- Certificado SSL (gestionado por el CT proxy)

# Flujo de instalación resumido

1. Crear CT a partir de plantilla LAMP.
2. Crear base de datos y usuario específicos.
3. Descargar PrestaShop 9.x y descomprimir en el DocumentRoot.
4. Ajustar permisos.
5. Completar el instalador web.
6. Eliminar la carpeta `/install`.
7. Configurar el virtual host y el proxy inverso (`ps-<tienda>.pm98.dj75.net`).

# Buenas prácticas

- No compartir el mismo CT entre tiendas no relacionadas.
- Mantener módulos y tema actualizados.
- Backups frecuentes (el CT completo + dump de la base de datos).
- Separar el entorno de desarrollo del de preproducción cuando el proyecto lo merezca.

# Relación con otros documentos

- [Stack PHP / LAMP](lamp-php.md)
- [LAMP](/desarrollo/lamp.md)

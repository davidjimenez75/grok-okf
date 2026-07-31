---
description: Plan de implementación por fases del servidor pm98.dj75.net.
generated:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - plan
  - implementacion
  - fases
title: Plan de implementación — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:35:00Z
  by: human:davidjimenez75
---

# Fase 1 — Host (1-2 días)

- Instalación de Proxmox VE 9.2 desde ISO.
- Configuración de hostname, red, ZFS/LVM-thin y repositorios.
- Actualización completa del sistema.
- Configuración de backups del host y de `vzdump`.
- Creación de token de API para automatización.
- Verificación de acceso seguro a la GUI (VPN recomendada).

# Fase 2 — Plantillas (1 día)

- Crear plantilla base `debian-13-dev`.
- Actualizar e instalar paquetes comunes.
- Crear plantillas derivadas: `debian13-dotnet`, `debian13-rust`, `debian13-lamp`.
- Documentar cómo regenerar las plantillas.

# Fase 3 — SQL Server (1 día)

- Crear VM Ubuntu 24.04 LTS.
- Instalar SQL Server 2025.
- Configurar usuarios, firewall (solo red interna) y backups de bases de datos.
- Probar conectividad desde un CT de prueba.

# Fase 4 — Contenedores de desarrollo (2-4 días)

- Desplegar CT proxy + configurar SSL y DNS.
- Crear al menos un CT de cada stack (.NET, Rust, LAMP, PrestaShop).
- Verificar flujos completos (compilación, conexión a SQL, instalación de PrestaShop, etc.).
- Ajustar recursos según uso real.

# Fase 5 — Estandarización y automatización

- Scripts o procedimientos para crear nuevos CTs a partir de plantilla.
- Etiquetado consistente en Proxmox.
- Documentación de cada CT dentro de este bundle OKF.
- Integración con los skills `proxmox-ops` y `container-ops`.
- Prueba de restauración completa de un CT y de la VM SQL.

# Criterios de aceptación

- Se puede crear un nuevo CT de cualquier stack en menos de 10 minutos.
- Todos los servicios web son accesibles por HTTPS con certificado válido.
- Los backups diarios se ejecutan sin errores y se ha verificado al menos una restauración.
- La documentación de este directorio `propuestas/pm98.dj75.net/` está actualizada.

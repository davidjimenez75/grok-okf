---
description: Configuración recomendada de contenedores Debian 13 para desarrollo con .NET 10 LTS.
generated:
  at: 2026-07-31T08:40:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - dotnet
  - csharp
  - stack
title: Stack .NET 10 — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:40:00Z
  by: human:davidjimenez75
---

# Versión objetivo

- **.NET 10** (LTS, soporte hasta noviembre 2028)
- Última patch disponible a julio 2026: serie 10.0.10 / SDK 10.0.302

# Contenedor recomendado

- Base: plantilla `debian13-dotnet` o instalación sobre `debian-13-dev`
- Recursos orientativos: 2-4 vCPU, 4-8 GB RAM, 40-80 GB disco

# Software a instalar

```bash
# Añadir repositorio Microsoft y paquetes
wget https://packages.microsoft.com/config/debian/13/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
dpkg -i packages-microsoft-prod.deb
apt update
apt install -y dotnet-sdk-10.0

# Herramientas adicionales útiles
dotnet tool install -g dotnet-ef
dotnet tool install -g dotnet-outdated-tool
```

# Capacidades del entorno

- Compilación y ejecución de aplicaciones .NET 10
- Entity Framework Core
- APIs REST / Minimal APIs
- Conexión a SQL Server (VM) y a MariaDB local si se necesita
- Soporte para desarrollo remoto (VS Code / Cursor via SSH)

# Buenas prácticas

- Usar `dotnet watch` durante el desarrollo.
- Mantener los `global.json` y `Directory.Build.props` versionados.
- No ejecutar como root dentro del CT.
- Separar CTs de «dev» y de «api/preview» cuando el proyecto lo requiera.

---
description: Comparativa de opciones de software para alojar repositorios Git bajo restricciones de 4 GB RAM en Debian 13.
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
title: Opciones de software — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Tabla comparativa rápida

| Opción                  | RAM aproximada | UI web          | Control acceso     | Complejidad | Recomendada en 4 GB |
|-------------------------|----------------|-----------------|--------------------|-------------|---------------------|
| Bare Git + SSH          | < 50 MB        | No (opcional cgit) | authorized_keys   | Muy baja    | **Sí (mejor)**      |
| Gitolite                | < 80 MB        | No              | Excelente (ACL)    | Baja        | **Sí**              |
| Soft Serve              | 20–60 MB       | TUI + SSH       | Claves SSH         | Baja        | **Sí**              |
| Forgejo / Gitea mínimo  | 150–400 MB     | Completa        | Usuarios/orgs      | Media       | Condicional         |
| GitLab                  | 4 GB+          | Completa        | Completo           | Alta        | **No**              |

# 1. Bare Git + SSH (opción mínima y más robusta)

**Descripción**: Repositorios bare (`git init --bare`) servidos únicamente por SSH. Los usuarios se autentican con claves públicas en `~git/.ssh/authorized_keys`.

**Ventajas**:
- Consumo de recursos prácticamente nulo.
- Máxima compatibilidad y fiabilidad.
- Paquetes 100 % oficiales de Debian (`git`, `openssh-server`).
- Fácil de respaldar (copiar directorio de repos).

**Desventajas**:
- Sin interfaz web nativa.
- Gestión de permisos manual (o con scripts).

**Ampliaciones ligeras**:
- `cgit` o `gitweb` + nginx/lighttpd para navegación de solo lectura.
- Script simple de creación de repos.

**Cuándo elegirla**: Cuando se prioriza estabilidad absoluta y se trabaja principalmente desde terminal / clientes Git.

# 2. Gitolite

**Descripción**: Capa de control de acceso sobre bare Git. Configuración centralizada en un repositorio `gitolite-admin`.

**Ventajas**:
- ACL granulares (lectura/escritura por repo y usuario/grupo).
- Muy maduro y ligero (Perl).
- Sigue siendo 100 % SSH.

**Desventajas**:
- Curva de aprendizaje inicial de la configuración.
- Sin UI web.

**Cuándo elegirla**: Si se necesita control de permisos fino sin añadir una aplicación web.

# 3. Soft Serve (Charmbracelet)

**Descripción**: Servidor Git moderno escrito en Go. Un solo binario. Acceso por SSH con TUI agradable, creación de repos, gestión de claves y usuarios desde la propia terminal.

**Ventajas**:
- Extremadamente ligero.
- Experiencia de usuario moderna sin web.
- Fácil de desplegar (binario o contenedor).

**Desventajas**:
- Proyecto más joven que Gitolite/Gitea.
- Sin interfaz web clásica (solo TUI sobre SSH).

**Cuándo elegirla**: Si se quiere algo moderno, agradable de usar y con muy poco overhead.

# 4. Forgejo / Gitea (configuración mínima)

**Descripción**: Forgejo es el fork comunitario activo de Gitea. Ambos son aplicaciones Go completas con issues, PRs, wiki, etc.

**Requisitos oficiales orientativos**: 1–2 núcleos y 512 MB–1 GB para equipos pequeños. En la práctica, con SQLite y features desactivadas puede bajar a ~150–300 MB en reposo.

**Ajustes obligatorios en 4 GB**:
- Usar **SQLite** (nunca PostgreSQL/MySQL).
- Desactivar o limitar: actions, packages, LFS si no se usa, mirror, etc.
- Reducir workers y concurrencia.
- Proxy inverso ligero (Caddy o nginx) en el mismo host o en otro CT si hubiera Proxmox.

**Ventajas**:
- Experiencia tipo GitHub completa.
- Gestión de usuarios, organizaciones, webhooks, etc.

**Desventajas**:
- Consume una parte significativa de los 4 GB.
- Más superficie de ataque y mantenimiento (actualizaciones, base de datos).

**Cuándo elegirla**: Solo si la UI web es imprescindible y se acepta que el sistema operará cerca del límite de memoria.

# 5. Opciones descartadas

- **GitLab**: requiere fácilmente 4–8 GB solo para sí mismo. Inviable.
- **OneDev / GitBucket**: Java → mayor consumo de RAM.
- **Gogs**: proyecto menos activo; Forgejo/Gitea son mejores opciones en 2026.

# Recomendación final por escenario

| Escenario                              | Opción recomendada          |
|----------------------------------------|-----------------------------|
| Uso personal, pocos repos, solo CLI    | Bare Git + SSH              |
| Varios usuarios / permisos finos       | Gitolite                    |
| Experiencia moderna sin web            | Soft Serve                  |
| Necesidad de UI web tipo GitHub        | Forgejo (mínimo) + ampliar RAM a 8 GB si es posible |

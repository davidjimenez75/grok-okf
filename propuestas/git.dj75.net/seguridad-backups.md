---
description: Política de seguridad y estrategia de backups para el servidor Git git.dj75.net.
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - seguridad
  - backups
  - git
title: Seguridad y backups — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
---

# Principios de seguridad

1. **Solo autenticación por clave SSH**. Deshabilitar login por contraseña (`PasswordAuthentication no`).
2. Usuario de servicio dedicado (`git`, `gitolite`, `softserve` o el usuario de Forgejo) sin shell interactivo innecesario.
3. Repositorios con permisos restrictivos (`700` o `750` según el modelo de acceso).
4. Actualizaciones de seguridad automáticas de Debian (`unattended-upgrades`).
5. Firewall restringido a la LAN.
6. Si se usa Forgejo/Gitea: mantenerlo actualizado y revisar periódicamente los permisos de los tokens de API.

# Hardening SSH

```bash
# /etc/ssh/sshd_config (extracto)
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AllowUsers git   # o la lista de usuarios necesarios
MaxAuthTries 3
```

Reiniciar `sshd` tras los cambios.

# Backups

Los repositorios Git son directorios. La estrategia más simple y efectiva es:

## Opción A — rsync / rclone periódico

```bash
# Ejemplo cron diario
0 3 * * * rsync -a --delete /var/lib/git/repositories/ /mnt/backup/git/
```

## Opción B — snapshots del sistema de archivos

Si se usa Btrfs o ZFS en el host:

- Snapshot diario del subvolumen/dataset que contiene los repos.
- Retención de 7–14 días + copias externas semanales.

## Opción C — bare mirror

Mantener un mirror bare en otra máquina (o en el NAS):

```bash
git clone --mirror git@git.dj75.net:proyecto.git
# y actualizar con git remote update
```

# Qué respaldar

| Elemento                    | Crítico | Notas                                      |
|-----------------------------|---------|--------------------------------------------|
| Directorio de repositorios  | Sí      | El contenido real                          |
| authorized_keys / config Gitolite | Sí | Control de acceso                          |
| Configuración Soft Serve / Forgejo | Sí | Usuarios, settings                         |
| Base de datos SQLite (Forgejo) | Sí   | Incluir en el mismo backup                 |
| Sistema operativo           | No      | Reinstalable fácilmente                    |

# Pruebas de restauración

Al menos una vez al trimestre:

1. Restaurar un repositorio en un directorio temporal.
2. Verificar que `git log` y `git fsck` funcionan.
3. Documentar el tiempo real de recuperación.

# Relación con playbooks existentes

- [Backup y restauración en Proxmox](/playbooks/backup-proxmox.md) (si el servicio corre dentro de un CT).
- [Respuesta a incidentes](/playbooks/respuesta-incidentes.md).

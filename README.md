# grok-okf

Bundle de conocimiento en **Open Knowledge Format (OKF) v0.2** con contenidos en español de España.

Orientado a programadores, desarrolladores y administradores de sistemas (Proxmox, contenedores, LAMP, Debian, grafos de conocimiento, skills de agente y propuestas de implementación).

## Estructura

```
.
├── index.md
├── log.md
├── conceptos/
├── sistemas/
├── desarrollo/
├── ingenieria-grafos/
├── skills/
├── propuestas/
│   ├── pm98.dj75.net/          # Servidor de desarrollo Proxmox + Debian 13
│   │   ├── resumen.md
│   │   ├── arquitectura.md
│   │   ├── host-proxmox.md
│   │   ├── contenedores.md
│   │   ├── red-dns.md
│   │   ├── seguridad-backups.md
│   │   ├── plan-implementacion.md
│   │   ├── recursos.md
│   │   └── stacks/
│   └── git.dj75.net/           # Servidor Git ligero (Q1900M, 4 GB RAM)
│       ├── resumen.md
│       ├── hardware.md
│       ├── opciones.md
│       ├── arquitectura.md
│       ├── red-dns.md
│       ├── seguridad-backups.md
│       ├── plan-implementacion.md
│       └── recursos.md
├── metricas/
└── playbooks/
```

## Características

- Frontmatter de todos los conceptos ordenado **alfabéticamente**.
- Contenidos redactados en español de España.
- Conforme a la especificación OKF v0.2.
- Incluye **propuestas completas** de servidores (pm98.dj75.net y git.dj75.net).

## Referencias

- [Especificación OKF](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)

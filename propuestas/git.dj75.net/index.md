---
description: Índice de la propuesta de servidor Git ligero git.dj75.net para intranet doméstica sobre Debian 13 y hardware Q1900M (4 GB RAM).
generated:
  at: 2026-07-31T15:20:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - git
  - debian13
  - bajo-recursos
title: Propuesta — git.dj75.net
type: Reference
verified:
  at: 2026-07-31T20:55:00Z
  by: agent:grok
---

# Propuesta: git.dj75.net

Servidor de repositorios Git para la **intranet doméstica**, orientado a hardware limitado (**ASRock Q1900M + Intel Celeron J1900 + 4 GB RAM**) y **Debian 13 (Trixie)**.

El objetivo es ofrecer varias opciones de complejidad y consumo de recursos, desde la más minimalista (solo SSH + bare repos) hasta forges completos (Forgejo/Gitea o GitLab CE), indicando claramente qué es viable según la cantidad de RAM disponible.

## Documentos de la propuesta

* [Resumen ejecutivo](resumen.md)
* [Hardware y restricciones](hardware.md)
* [Opciones de software (comparativa)](opciones.md)
* [Arquitectura recomendada](arquitectura.md)
* [Red y DNS](red-dns.md)
* [Seguridad y backups](seguridad-backups.md)
* [Plan de implementación](plan-implementacion.md)
* [Estimación de recursos](recursos.md)

## Opciones de software (detalle individual)

* [Bare Git + SSH](opciones/bare-git-ssh.md)
* [Gitolite](opciones/gitolite.md)
* [Soft Serve](opciones/soft-serve.md)
* [Forgejo / Gitea](opciones/forgejo.md)
* [GitLab CE](opciones/gitlab.md)

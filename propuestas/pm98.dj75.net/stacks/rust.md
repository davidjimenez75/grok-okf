---
description: Configuración de contenedores Debian 13 para desarrollo con Rust (toolchain estable).
generated:
  at: 2026-07-31T08:40:00Z
  by: human:davidjimenez75
status: stable
tags:
  - propuesta
  - rust
  - cargo
  - stack
title: Stack Rust — pm98.dj75.net
type: Reference
verified:
  at: 2026-07-31T08:40:00Z
  by: human:davidjimenez75
---

# Versión objetivo

- Rust **stable 1.97.1** (julio 2026) o la stable vigente en el momento de la instalación
- Instalación vía `rustup` (método oficial y más flexible)

# Contenedor recomendado

- Base: plantilla `debian13-rust` o `debian-13-dev`
- Recursos orientativos: 2-4 vCPU, 4-8 GB RAM, 40-60 GB disco

# Instalación típica

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
rustup default stable
rustup component add clippy rustfmt

# Herramientas adicionales útiles
cargo install cargo-watch cargo-edit cargo-outdated
```

# Capacidades del entorno

- Compilación de binarios y librerías
- Desarrollo de CLIs, servicios y herramientas de sistemas
- Integración con bases de datos (SQL Server vía crates, MariaDB, etc.)
- Uso de `mold` o `lld` como linker para acelerar compilaciones (opcional)

# Buenas prácticas

- Mantener `rust-toolchain.toml` en cada proyecto para fijar la versión.
- Usar `cargo watch` durante el desarrollo.
- Separar CTs por proyecto grande si el directorio `target/` crece mucho.
- Limpiar `target/` periódicamente o usar `sccache` si se comparte entre CTs.

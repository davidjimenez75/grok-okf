---
description: Interfaz web de terminal/SSH (ttyd) que permite interactuar directamente con Grok al conectarse vía navegador.
generated:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
status: draft
tags:
  - propuesta
  - web-terminal
  - ttyd
  - ssh
  - grok
title: Interfaz web SSH/terminal — grok.dj75.net
type: Reference
verified:
  at: 2026-08-01T08:30:00Z
  by: agent:grok
---

# Objetivo de la interfaz

Cuando un usuario abre `https://grok.dj75.net` debe obtener una **terminal en el navegador** que le permita interactuar **directamente con Grok**, sin necesidad de instalar clientes SSH ni configurar claves localmente.

# Tecnología recomendada: ttyd

**ttyd** es la opción preferida por:

- Ser extremadamente ligero.
- Soportar WebSockets de forma nativa.
- Permitir ejecutar un comando arbitrario al arrancar la sesión.
- Tener buen soporte de autenticación básica y certificados.
- Estar disponible como binario o empaquetable fácilmente en Debian.

Alternativas aceptables: wetty, shellinabox (más antiguo), o incluso code-server si se desea un IDE completo.

# Arranque de la sesión

El servicio ttyd se configura para lanzar un comando personalizado, por ejemplo:

```bash
ttyd --port 7681 --credential usuario:hash \
  /opt/grok-agent/bin/grok-shell
```

Donde `grok-shell` puede ser:

- Un script que inicia un REPL de chat con Grok (entrada → API → respuesta en la terminal).
- Una shell bash normal con el entorno ya cargado (`source /opt/grok-agent/env.sh`) y un alias/prompt que indica que se está hablando con Grok.
- Un wrapper que combina ambos (modo chat + modo shell).

# Experiencia de usuario deseada

1. El usuario llega a `https://grok.dj75.net`.
2. Se autentica (basic auth del proxy o de ttyd).
3. Aparece una terminal limpia.
4. Puede escribir en lenguaje natural y Grok responde, o ejecutar comandos del sistema.
5. El agente tiene acceso a las herramientas del contenedor y puede mostrar resultados, editar ficheros, etc.

# Configuración del proxy

El CT proxy (Caddy o Nginx) debe:

- Terminar TLS (Let’s Encrypt o certificado interno).
- Reenviar el tráfico (incluyendo WebSockets) al puerto 7681 del CT grok.
- Aplicar autenticación adicional si se desea (basic, forward-auth, etc.).

Ejemplo conceptual con Caddy:

```
grok.dj75.net {
    basicauth {
        usuario hash_bcrypt
    }
    reverse_proxy ct-grok-01:7681
}
```

# Acceso SSH clásico (opcional)

Se mantiene OpenSSH para administración directa:

- Solo autenticación por clave pública.
- fail2ban o equivalente.
- Puerto no estándar si se quiere (o solo accesible desde la red interna).

# Seguridad de la interfaz web

- Siempre detrás de HTTPS.
- Autenticación obligatoria.
- Rate limiting en el proxy.
- Timeout de sesión inactiva.
- No exponer el puerto de ttyd directamente a Internet (solo a través del proxy).

---
description: Lenguaje de programación interpretado del lado del servidor, ampliamente usado en la web y base del stack LAMP.
generated:
  at: 2026-07-31T07:40:00Z
  by: human:davidjimenez75
status: stable
tags:
  - php
  - programacion
  - web
  - lamp
  - backend
title: PHP
type: Reference
verified:
  at: 2026-07-31T07:40:00Z
  by: human:davidjimenez75
---

# Definición

**PHP** (PHP: Hypertext Preprocessor) es un lenguaje de programación de propósito general orientado especialmente al desarrollo web del lado del servidor. Se ejecuta en el servidor y genera HTML dinámico.

Es el lenguaje más usado en la web junto con JavaScript, y la base de proyectos como WordPress, Laravel, Symfony, Drupal, etc.

# Versiones recomendadas (2026)

- **PHP 8.3 / 8.4**: versiones activas con mejoras de rendimiento, tipado y sintaxis moderna.
- Evitar PHP 7.x (fin de soporte de seguridad).

# Características útiles modernas

- Tipado estricto (`declare(strict_types=1);`)
- Named arguments, attributes, enums, fibers, JIT
- Composer como gestor de dependencias estándar
- PSR (PHP Standards Recommendations) para interoperabilidad

# Ejemplo mínimo moderno

```php
<?php
declare(strict_types=1);

namespace App;

final class Greeter
{
    public function __construct(
        private readonly string $name
    ) {}

    public function greet(): string
    {
        return "Hola, {$this->name}";
    }
}

echo (new Greeter('David'))->greet();
```

# Buenas prácticas

- Usar siempre `declare(strict_types=1);`.
- Preferir frameworks modernos (Laravel, Symfony) o al menos una estructura MVC clara.
- Gestionar dependencias con Composer.
- Evitar `mysql_*` (obsoleto); usar PDO o mysqli con prepared statements.
- Configurar `error_reporting` y logs adecuadamente en producción (`display_errors = Off`).
- Usar OPcache y, si es posible, JIT en PHP 8+.

# Enlaces útiles

- Documentación oficial: https://www.php.net/docs.php
- PHP The Right Way: https://phptherightway.com/
- Packagist (Composer): https://packagist.org/

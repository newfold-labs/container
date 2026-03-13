# Getting started

## Prerequisites

- **PHP** 7.0+ (see `composer.json`).
- **Composer**.

## Install

From the package root:

```bash
composer install
```

No production dependencies other than PHP.

## Minimal usage

```php
use NewfoldLabs\Container\Container;

$container = new Container();
$container->set( 'plugin', $plugin_instance );
$container->set( 'cache_types', [ 'browser', 'skip404' ] );
$container->set( 'my_service', $container->service( function ( $c ) {
    return new MyService( $c->get( 'plugin' ) );
} ) );

$service = $container->get( 'my_service' ); // same instance each time
```

See [integration.md](integration.md) for how the loader and host plugins use the container.

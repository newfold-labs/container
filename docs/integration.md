---
name: container
title: Integration
description: How the module registers and integrates.
updated: 2025-03-18
---

# Integration

## How the loader uses the container

**wp-module-loader** depends on `newfold-labs/container`. The host plugin (e.g. Bluehost) creates a container, registers the plugin instance and any config (e.g. brand, cache types, marketplace brand), then passes it to the loader via `NewfoldLabs\WP\ModuleLoader\container( $container )`. The loader extends the container as `NewfoldLabs\WP\ModuleLoader\Container` (adding `plugin()`) and uses it when running each module’s callback: `$module->callback( container(), $module )`.

So the host never instantiates the loader’s extended container directly; it instantiates the base `NewfoldLabs\Container\Container` (or the loader’s `Container` which extends it), sets entries, then calls `container( $container )` so the loader and all modules share that instance.

## Typical host setup

1. Create container: `$container = new \NewfoldLabs\Container\Container();` (or the loader’s extended class).
2. Set plugin and config: `$container->set( 'plugin', new Plugin( ... ) );`, `$container->set( 'cache_types', ... );`, etc.
3. Set the container on the loader: `\NewfoldLabs\WP\ModuleLoader\container( $container );`
4. Load modules (via Composer autoload); they register with the loader and receive `container()` in their callback.

## Where context lives

Context (brand, platform) is not stored in the container; it is provided by **wp-module-context** via `setContext()` / `getContext()`. The runtime (wp-module-runtime) reads from the container (e.g. `capabilities`) and from filters (e.g. `newfold_runtime`) to build `window.NewfoldRuntime`.

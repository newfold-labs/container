---
name: container
title: Overview
description: What the module does and who maintains it.
updated: 2025-03-18
---

# Overview

## What this package does

**newfold-labs/container** is a small PSR-11-compatible dependency injection container. It is used by the Newfold Module Loader and by WordPress brand plugins (e.g. Bluehost) to hold shared state (plugin instance, capabilities, cache types, etc.) and to provide services/factories so modules receive the same container instance.

- **PSR-11:** Implements `ContainerInterface` (`get`, `has`). Throws `NotFoundException` when an entry is missing.
- **Entries:** Set with `set( $id, $value )`. Values can be raw, or wrapped with `service( Closure )` (singleton per id) or `factory( Closure )` (new instance each time). Also supports `computed( Closure )` for one-off computation.
- **ArrayAccess & Iterator:** The container implements `ArrayAccess` and `Iterator` for convenience.

## Who maintains it

- **Newfold Labs** (Newfold Digital). Distributed via Newfold Satis. Used by wp-module-loader and all Newfold WordPress brand plugins.

## High-level features

- `get( $id )`, `has( $id )`, `set( $id, $value )`, `raw( $id )`, `delete( $id )`
- `service( Closure )` – resolve once per id and reuse
- `factory( Closure )` – resolve every time
- `extend( $id, Closure )` – wrap an existing factory/service
- `keys()`, `count()`, iteration

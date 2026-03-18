# Agent guidance – newfold-labs/container

This file gives AI agents a quick orientation to the repo. For full detail, see the **docs/** directory.

## What this project is

- **newfold-labs/container** – Lightweight, PSR-11-compatible dependency injection container used by the Newfold Module Loader and brand plugins. Supports get/set, factories (new instance each time), services (singleton per id), and computed values. Implemented in PHP with no framework dependencies. Maintained by Newfold Labs.

- **Stack:** PHP 7.0+ (see `composer.json`). No frontend; consumed as a Composer dependency by wp-module-loader and host plugins.

- **Architecture:** Host or loader instantiates `NewfoldLabs\Container\Container`, registers entries with `set()`, `service()`, or `factory()`, then passes the container to the loader. The wp-module-loader extends this container and uses it to provide the plugin instance and other shared state to modules.

## Key paths

| Purpose | Location |
|---------|----------|
| Container implementation | `includes/Container.php` |
| PSR-11 interface | `includes/ContainerInterface.php` |
| Exceptions | `includes/ContainerException.php`, `includes/NotFoundException.php` and interfaces |

## Essential commands

```bash
composer install
```

No test or lint scripts in this repo.

## Documentation

- **Full documentation** is in **docs/**. Start with **docs/index.md**.
- **CLAUDE.md** is a symlink to this file (AGENTS.md).

---

## Keeping documentation current

**When you change code, features, or workflows, update the docs so they stay accurate.** Keep **docs/index.md** current: when you add, remove, or rename doc files, update the table of contents (and quick links if present).

- Keep all docs current, not only the ones listed here.
- Prefer updating the appropriate file(s) in **docs/** over leaving docs out of date.
- When adding or changing the public API, update **docs/integration.md** or **docs/overview.md**. When cutting a release, update **docs/changelog.md** if the repo is released.

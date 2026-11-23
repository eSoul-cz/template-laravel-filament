<!-- esoul-guidelines:begin frontend -->
# Project guidelines - Frontend

## Stack

Vite builds the frontend assets, styled with Tailwind CSS, on Node with pnpm. `package.json` and its lockfile are authoritative for versions ([tools.md](tools.md#versions)).

A Filament admin panel is a separate user interface: the Inertia and Vue rules do not apply to it. Only the Vite, Tailwind CSS and command rules of this file hold for its theme.

## Vite and bundling

- Vite builds the frontend assets with the Laravel plugin (`@vite` in Blade views, the Laravel Vite entry points); `pnpm build` is part of CI.

## Tailwind CSS

- Tailwind CSS, configured CSS-first in `resources/css/app.css` (the version is in [tools.md](tools.md#versions)); no JavaScript Tailwind configuration and no deprecated utilities of earlier majors.
- Colours, type, spacing and radii come from the semantic design tokens declared in `app.css` (`@theme`), which mirror the project's design source. Use semantic colours (`bg-background`, `text-foreground`, `text-muted-foreground`, `border-border`); no hex values and no arbitrary values where a token or a standard utility exists.
- New UI works at the application's responsive breakpoints and, when the project supports dark mode, in dark mode.
- Global CSS is limited to tokens, base styles and genuinely global behaviour.

<!-- from: package/filament -->
- A Filament panel is themed with a Filament theme: a CSS file built by Vite and registered on the panel (`viteTheme()`), generated with `php artisan make:filament-theme --pm=pnpm` (without the option Filament uses npm and creates an npm lockfile). The theme and the application's own Blade views follow the Tailwind token rules of this file (tokens in `app.css`, semantic colours, no arbitrary values); the design-system and Vue rules do not apply to them.
- Colours come from the panel's colour configuration and the semantic design tokens, not from hex values in the theme; a utility class does not override a Filament component's internals where a panel option, a colour or a theme token exists.

## Frontend commands

- pnpm is the only package manager ([dependencies.md](dependencies.md#pnpm-repositories)).
- Vite builds the assets: `pnpm dev` serves them during development and `pnpm build` produces the production build that CI runs ([deployment.md](deployment.md#pipeline)).

> Local additions go below this managed block. Content outside the block is preserved when the guidelines are synced.
<!-- esoul-guidelines:end frontend -->

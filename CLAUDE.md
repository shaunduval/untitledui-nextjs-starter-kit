# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Untitled UI Next.js starter kit - a React component library built with Next.js 16, React 19, TypeScript, Tailwind CSS v4, and React Aria for accessibility.

## Commands

```bash
bun dev       # Start dev server with Turbopack (localhost:3000)
bun build     # Production build
bun start     # Run production server
bun lint      # Check for lint/format issues
bun lint:fix  # Auto-fix lint/format issues
bun format    # Format all files
```

Linting and formatting handled by Ultracite (Biome). Config in `biome.jsonc`.

## Architecture

### Component Structure

Components are organized in `src/components/` by usage context:
- **base/** - Core reusable components (buttons, inputs, checkboxes, selects, etc.)
- **application/** - App-level components (modals, tables, navigation, pagination)
- **marketing/** - Landing page components
- **foundations/** - Design tokens, logos, icons (social, payment, featured)
- **shared-assets/** - Illustrations, patterns, QR codes

### Styling Pattern

Components use a consistent styling approach with `sortCx` for organized Tailwind classes:

```typescript
export const styles = sortCx({
  common: { root: [...], icon: [...] },
  sizes: { sm: {...}, md: {...}, lg: {...}, xl: {...} },
  colors: { primary: {...}, secondary: {...} }
});

// In component:
className={cx(styles.common.root, styles.sizes[size].root, styles.colors[color].root, className)}
```

- `cx` (from `@/utils/cx`) - wraps tailwind-merge for class merging
- `sortCx` - organizes styles as objects for IntelliSense support

### Key Patterns

- **"use client"** - Required for interactive components
- **React Aria** - Components extend React Aria for accessibility (keyboard nav, ARIA attributes, focus management)
- **Theme** - CSS variables in `src/styles/theme.css`, dark mode via next-themes with class-based approach
- **Path alias** - `@/*` maps to `./src/*`

### Providers

Root layout (`src/app/layout.tsx`) wraps with:
- `RouteProvider` - Router context
- `Theme` - Dark/light mode via next-themes

## Linting & Formatting

Uses Ultracite with Biome (`biome.jsonc`):
- Zero-config preset for Next.js
- Run `bun lint:fix` to auto-fix issues

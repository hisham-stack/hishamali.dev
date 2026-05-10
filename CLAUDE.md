# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

## Project

Personal portfolio site for Hisham Ali, Full-Stack Developer. Deployed to Vercel.

## Commands

```bash
pnpm dev          # start dev server
pnpm build        # production build
pnpm start        # serve production build
pnpm lint         # eslint + tsc --noEmit
pnpm format       # prettier --write .
pnpm format:check # prettier --check .
pnpm analyze      # bundle analysis (ANALYZE=true next build)
```

No test suite is configured yet.

## Stack & Key Versions

- **Next.js 16.2.6** — App Router. APIs may differ from training data; read `node_modules/next/dist/docs/` before writing code.
- **React 19.2.4**
- **Tailwind CSS v4** — configured via `@tailwindcss/postcss`; v4 has breaking changes from v3 (no `tailwind.config.js`, utility syntax changes).
- **TypeScript** — strict; `tsc --noEmit` is part of `pnpm lint`.
- **pnpm** — use `pnpm` for all package operations.

## Code Style

Prettier enforces: single quotes, no semicolons, 2-space indent, trailing commas (ES5), Tailwind class sorting. Run `pnpm format` before committing.

ESLint uses the v9 flat config (`eslint.config.mjs`) with `eslint-config-next` core-web-vitals + TypeScript presets.

The `docs/design/prototype/` directory contains raw HTML/JSX prototype files and is excluded from both ESLint and Prettier.

## Architecture

App Router layout: `app/layout.tsx` is the root layout with Geist/Geist Mono fonts and a flex column body. `app/page.tsx` is the home page. Global styles are in `app/globals.css`.

The design prototype in `docs/design/prototype/` (Portfolio.html + components.jsx) serves as the visual reference for the actual implementation. Consult it when building UI components.

## Product Requirements

Full PRD is in `docs/prd.md` — read it before implementing any page or component.
Key sections:
- §8 — design tokens (colours, typography, spacing)
- §7 — page specifications
- §10 — technical architecture
- §16.6 — commit sequence (follow this order)

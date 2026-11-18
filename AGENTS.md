# Repository Guidelines

printIT is a small public print catalog with admin login. The runnable app is still the `10x-astro-starter` tree (Astro 7 SSR, React 19, TypeScript, Tailwind 4, Supabase, Cloudflare) and it is not at the repository root. Product intent is `@context/foundation/prd.md`. The stack decision is `@context/foundation/tech-stack.md`.

## Hard rules

Run npm scripts from `.bootstrap-scaffold/`. The root has no `package.json`. The starter was cloned there and never merged; `@context/changes/bootstrap-verification/verification.md` records that. Do not move, delete, or `git add` that directory unless asked. It contains `node_modules` and its own `.git`.

Do not write under `context/archive/`.

Use Node `22.14.0` (`@.bootstrap-scaffold/.nvmrc`). `astro@7` requires `>=22.12.0`. The logged `npm install` ran on Node v20.12.2 and only warned `EBADENGINE`.

Keep `SUPABASE_URL` and `SUPABASE_KEY` out of git. Copy `@.bootstrap-scaffold/.env.example` to `.bootstrap-scaffold/.env` or `.bootstrap-scaffold/.dev.vars`. Do not commit either file.

App conventions are `@.bootstrap-scaffold/CLAUDE.md`. `@.bootstrap-scaffold/AGENTS.md` contains only the line `CLAUDE.md`. Root `@CLAUDE.md` is the lesson router, not the app.

## Commands

From `.bootstrap-scaffold/`:

- `npm run dev` — Cloudflare workerd dev server.
- `npm run lint` — ESLint. `npm run lint:fix` applies fixes. `npm run format` runs Prettier.
- `npm run build` — production SSR build. Requires `SUPABASE_URL` and `SUPABASE_KEY`.
- `npm run preview` — serve that build.
- `npm run smoke` — only scripted test: auth flow in `@.bootstrap-scaffold/scripts/smoke.mjs` against a running server. `BASE_URL` defaults to `http://localhost:4321`.

Husky plus `lint-staged` in `@.bootstrap-scaffold/package.json` runs `eslint --fix` on `*.{ts,tsx,astro}` and `prettier --write` on `*.{json,css,md}`.

## Where code and docs live

- `.bootstrap-scaffold/src/pages/` — pages and `api/` routes. `output` is `"server"` in `@.bootstrap-scaffold/astro.config.mjs`.
- `.bootstrap-scaffold/src/middleware.ts` — session on every request. `PROTECTED_ROUTES` is `["/dashboard"]`; other paths stay public.
- `.bootstrap-scaffold/src/components/` — Astro chrome and React auth islands. shadcn UI is under `ui/`.
- `.bootstrap-scaffold/src/lib/` — Supabase client and helpers. `@/*` maps to `./src/*` in `@.bootstrap-scaffold/tsconfig.json`.
- `context/foundation/` — `prd.md`, `tech-stack.md`, `shape-notes.md`. `context/changes/` — one folder per in-flight change.
- Catalog pages from the PRD are absent. `src/pages/` is still `index`, `auth/*`, and `dashboard`.

## CI and commits

`@.bootstrap-scaffold/.github/workflows/ci.yml` triggers on push and pull request to `master`: `npm ci`, `npx astro sync`, `npm run lint`, `npx astro check`, `npm run build` (secrets `SUPABASE_URL`, `SUPABASE_KEY`), then a smoke job on local Supabase. The printIT root has no `.github/workflows/`.

Root commits are one capitalized sentence and no type prefix (`Initial commit`, then bootstrap-log notes). Match that. Remote: `https://github.com/NataliaSoltys/printIT.git`. Do not commit or push from the nested starter `.git`.

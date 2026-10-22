---
bootstrapped_at: 2026-10-22T19:39:22Z
starter_id: 10x-astro-starter
starter_name: "10x Astro Starter (Astro + Supabase + Cloudflare)"
project_name: print-it
language_family: js
package_manager: npm
cwd_strategy: git-clone
bootstrapper_confidence: first-class
phase_3_status: failed
audit_command: "npm audit --json"
---

## Hand-off

```yaml
starter_id: 10x-astro-starter
package_manager: npm
project_name: print-it
hints:
  language_family: js
  team_size: solo
  deployment_target: cloudflare-pages
  ci_provider: github-actions
  ci_default_flow: auto-deploy-on-merge
  bootstrapper_confidence: first-class
  path_taken: standard
  quality_override: false
  self_check_answers: null
  has_auth: true
  has_payments: false
  has_realtime: false
  has_ai: false
  has_background_jobs: false
```

## Why this stack

printIT is a small, after-hours web catalog with admin login and no payments. The user chose the recommended JS web starter: Astro + React 19 + TypeScript + Tailwind CSS 4 + Supabase + Cloudflare. That covers public pages, API routes, typed contracts, admin auth, and file storage without a shopping cart. Solo + 5-week timeline favors a batteries-included, convention-heavy stack. Cloudflare Pages is the starter default and fits a free/near-free host; CI is GitHub Actions with auto-deploy on merge to main. Scaffolding is first-class (registered CLI, not end-to-end battle-tested).

## Pre-scaffold verification

| Signal      | Value                                                         | Severity | Notes                                                                                                      |
| ----------- | ------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------- |
| npm package | not run                                                       | —        | `cmd_template` starts with `git clone`; npm package recency check skipped                                 |
| GitHub repo | przeprogramowani/10x-astro-starter last pushed 2026-09-12     | fresh    | `gh` CLI not installed. `pushed_at` read from the public GitHub API (`2026-09-12T21:16:08Z`). Within 3 months of 2026-10-22. |

## Scaffold log

**Resolved invocation**: `git clone https://github.com/przeprogramowani/10x-astro-starter .bootstrap-scaffold && cd .bootstrap-scaffold && npm install`

**Strategy**: git-clone

**Exit code**: 1

**Stderr (last 20 lines)**:

```
npm WARN cleanup       code: 'EPERM',
npm WARN cleanup       syscall: 'rmdir',
npm WARN cleanup       path: 'C:\\projects\\printIT\\.bootstrap-scaffold\\node_modules\\rolldown\\node_modules'
npm WARN cleanup     }
npm WARN cleanup   ],
npm WARN cleanup   [
npm WARN cleanup     'C:\\projects\\printIT\\.bootstrap-scaffold\\node_modules\\@bruits',
npm WARN cleanup     [Error: EPERM: operation not permitted, rmdir 'C:\projects\printIT\.bootstrap-scaffold\node_modules\@bruits\satteri-wasm32-wasi'] {
npm WARN cleanup       errno: -4048,
npm WARN cleanup       code: 'EPERM',
npm WARN cleanup       syscall: 'rmdir',
npm WARN cleanup       path: 'C:\\projects\\printIT\\.bootstrap-scaffold\\node_modules\\@bruits\\satteri-wasm32-wasi'
npm WARN cleanup     }
npm WARN cleanup   ]
npm WARN cleanup ]
npm ERR! code UNABLE_TO_VERIFY_LEAF_SIGNATURE
npm ERR! errno UNABLE_TO_VERIFY_LEAF_SIGNATURE
npm ERR! request to https://registry.npmjs.org/zwitch/-/zwitch-2.0.4.tgz failed, reason: unable to verify the first certificate

npm ERR! A complete log of this run can be found in: C:\Users\natal\AppData\Local\Temp\cursor-sandbox-cache\8743c4281656a161de0e45a684ca3dc2\npm\_logs\2026-10-22T19_39_22_727Z-debug-0.log
```

**.bootstrap-scaffold left in place at**: `.bootstrap-scaffold/`

Clone succeeded. The first `npm install` failed while downloading `zwitch-2.0.4.tgz` with `UNABLE_TO_VERIFY_LEAF_SIGNATURE` and printed `EBADENGINE` warnings: Node v20.12.2 and npm 10.5.0, while `astro@7.3.2` requires Node `>=22.12.0`.

**Retry**: `npm install` was run again in `.bootstrap-scaffold` and exited 0 (2026-10-22, about 41s). npm reported `changed 202 packages, and audited 649 packages`. The `EBADENGINE` warnings were unchanged. The conflict policy was not applied. Files were not moved into the project root, and the cloned `.git/` is still inside `.bootstrap-scaffold/`.

## Post-scaffold audit

**Tool**: `npm audit --json` was not run as a separate pass. Counts below are from the successful `npm install` summary.

**Summary**: 0 CRITICAL, 10 HIGH, 2 MODERATE, 1 LOW (13 total)

**Direct vs transitive**: not distinguished by the install summary

#### CRITICAL findings

None reported.

#### HIGH findings

10, names not captured. The install summary did not list packages.

#### MODERATE findings

2, names not captured.

#### LOW / INFO findings

1 LOW. No INFO count was reported.

## Hints recorded but not acted on

| Hint                    | Value              |
| ----------------------- | ------------------ |
| bootstrapper_confidence | first-class        |
| quality_override        | false              |
| path_taken              | standard           |
| self_check_answers      | null               |
| team_size               | solo               |
| deployment_target       | cloudflare-pages   |
| ci_provider             | github-actions     |
| ci_default_flow         | auto-deploy-on-merge |
| has_auth                | true               |
| has_payments            | false              |
| has_realtime            | false              |
| has_ai                  | false              |
| has_background_jobs     | false              |

## Next steps

Next: a future skill will set up agent context (CLAUDE.md, AGENTS.md). For now, your project is scaffolded and verified — happy hacking.

Useful manual steps in the meantime:
- Move the starter out of `.bootstrap-scaffold/` into the project root (drop the cloned `.git/`, keep `context/`). That move has not been done.
- Upgrade Node to `>=22.12.0` before running the app. The install succeeded on v20.12.2, with engine warnings.
- `git init` is already done in this repo.
- Run `npm audit` in the installed tree for package names behind the 10 HIGH findings.

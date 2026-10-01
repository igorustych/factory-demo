# Agent instructions

## Project overview

Launchpad is a local-first developer portal for a workshop. It reads fictional,
committed service data and runbooks; it is not a live service directory or CI
integration. Keep the UI read-only and do not add runtime network calls,
credentials, telemetry, external fonts, or live-service claims.

This checkout is the `workshop-starter` checkpoint. The Docs Site `never` CI
snapshot intentionally displays as **Passing** as a disclosed workshop defect.
Preserve that behavior unless the task specifically asks to complete the
status-fix exercise. Do not implement features from later workshop checkpoints
unless requested.

## Setup and commands

- Use Node `22.22.3` as pinned in `.nvmrc`; the project expects npm `10.9.8`.
- Install the committed dependencies with `npm ci`.
- Start the local app with `npm run dev`. Vite binds to
  `http://127.0.0.1:5173` and refuses to silently use a different port.
- If that port is occupied, choose one explicitly:
  `npm run dev -- --port 5174`.
- Check TypeScript with `npm run typecheck`.
- Create the production build with `npm run build`.
- To inspect the built app, run `npm run preview` after the build. It serves on
  `http://127.0.0.1:4173`.

Run `npm run typecheck` and `npm run build` after code or data changes. This
checkpoint has no `test`, `lint`, or aggregate `check` script; do not report
those commands as available or passing.

## Code and data conventions

- Keep domain rules in `src/domain/` and presentation in `src/`. The app loads
  and validates its fixtures through `src/data/load.ts` and
  `src/domain/catalog.ts`.
- Shared service records live in `data/catalog.json`, CI examples in
  `data/ci-snapshots.json`, and the Markdown runbooks in `data/runbooks/`.
  Update the validated schema and relevant fixtures together when changing the
  data contract. Keep the fixed sample timestamp; do not substitute the current
  time.
- Preserve strict TypeScript checks. Avoid unsafe casts and keep types aligned
  with the Zod-validated data.
- Keep runbooks local and render Markdown as text/content, not executable HTML.
  Do not introduce unsafe links, path traversal, or raw HTML rendering.
- Keep the app read-only. Do not add localStorage writes, background updates,
  accounts, a database, or external integrations.
- Preserve accessibility and responsive behavior when changing the UI. Status
  must remain understandable without color alone.
- Follow existing formatting and component patterns; keep changes scoped to
  the requested task.

## Git and validation workflow

- Inspect `git status` and the diff before changing or staging files. Treat
  existing and untracked files as user work; do not reset, clean, or discard
  them.
- Keep dependencies, build output, coverage, Playwright output, `.presenter/`,
  and `.workshop-output/` out of commits. Do not force-add ignored files.
- Before finishing, review the complete diff and report the exact validation
  commands run, their results, and any checks this checkpoint does not provide.

# Acquisitions API agent rules
## Project overview
- Node.js ESM backend API (`type: module`) with Express 5.
- Main entrypoint is `src/index.js`, which loads env and starts `src/server.js`.
- Layering pattern:
  - Routes in `src/routes`
  - Controllers in `src/controllers`
  - Business logic in `src/services`
  - Validation in `src/validations`
  - DB schema/config in `src/models` and `src/config/database.js`
  - Shared helpers in `src/utils`

## Import and module conventions
- Prefer path aliases from `package.json#imports` (for example `#services/*`, `#utils/*`) over long relative imports.
- Keep files as ES modules (`import`/`export`), not CommonJS.

## Code style and formatting
- Follow `.prettierrc`: single quotes, semicolons, 2-space indentation, print width 80, LF line endings.
- Respect `eslint.config.js` rules (`prefer-const`, `no-var`, no unused vars unless prefixed with `_`, etc.).
- Keep changes focused; avoid unrelated refactors in the same edit.

## Validation and safety
- For request/response changes, update validation schemas and route/controller wiring together.
- Never hardcode secrets. Read secrets from environment variables.
- Do not modify `.env` values in automation unless explicitly asked.

## Commands to validate changes
- Lint: `npm run lint`
- Format check: `npm run format:check`
- Dev server: `npm run dev`
- Drizzle tasks: `npm run db:generate`, `npm run db:migrate`, `npm run db:studio`

## Scope guardrails
- Treat `logs/` as runtime output; do not edit logs to satisfy tasks.
- Only modify `drizzle/` migration output when the task explicitly involves schema migration artifacts.

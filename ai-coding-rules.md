# AI Coding Rules for BookShelf

Read `docs/v1-spec.md` before every task. If a rule here conflicts with the spec, stop and ask. Never add a feature that is not in the spec's Must or Should list.

## Folder structure
```
src/app/            routes only: page.tsx, layout.tsx, route.ts. No business logic.
src/features/{library,import,ai-summary,feedback,auth,covers}/   components, actions.ts, queries.ts, schema.ts
src/components/     shared presentational components. No data access.
src/lib/            pure functions with no I/O: normalize, parse-import, stats, placeholder, genres
src/server/         server-only code: supabase clients, llm, lookup providers, rate-limit, env
src/themes/         theme types, registry, one folder per theme
supabase/migrations/  numbered SQL files, never edited after merge
public/themes/{id}/ theme assets
tests/              unit (Vitest) and e2e (Playwright)
```

## Naming
- Files and folders: `kebab-case`. React components: `PascalCase` named exports. Functions and variables: `camelCase`. Types: `PascalCase`. Constants: `SCREAMING_SNAKE_CASE`. Database tables and columns: `snake_case`.
- Boolean names start with `is`, `has` or `can`. Server actions end with `Action`.

## TypeScript
- `strict: true`, `noUncheckedIndexedAccess: true`, `noImplicitOverride: true`.
- `any`, `@ts-ignore`, `@ts-expect-error` without a linked issue, and non-null assertions (`!`) are forbidden.
- Every input from a request, form, URL, `localStorage`, or external API is parsed with zod before use. Types are inferred from zod schemas.

## Secrets and server-only code
- Every file in `src/server/**` starts with `import "server-only"`.
- Read environment variables only through `src/server/env.ts`. Never use a secret in a file that has `"use client"`. Only `NEXT_PUBLIC_` variables may reach the browser.
- The LLM is called only through `generateStructured` in `src/server/llm/index.ts`. Never import a provider SDK anywhere else.

## Database access
- Every table has RLS enabled. Add the policy in the same migration that creates the table.
- Use the user-session Supabase client by default. Use the service-role client only in `src/server/supabase/admin.ts` callers listed in spec section 12.5.
- Select explicit columns; never `select('*')`. The public page uses the anon client without cookies.
- All reads and writes of `library_books` go through `src/features/library/queries.ts` and `actions.ts`.
- Schema changes are new migration files only.

## Forbidden shortcuts
- No hardcoded colors, fonts, or `/themes/` paths outside `src/themes/**` and `public/themes/**`.
- No `localStorage` access outside the two keys named in the spec (`bookshelf.importDraft.v1`, `bookshelf.feedback.v1`).
- No `dangerouslySetInnerHTML`, no `eval`, no disabling lint rules with comments.
- No new npm dependency without a one-line justification in the commit message; prefer the platform API.
- No game engine or canvas for the shelf. No AI call inside the import parser.
- No `console.log` in committed code; use the logger with a request id.
- No catch block that swallows an error.
- No copy text invented in code: use the exact strings from the spec.

## Commit policy
- One commit per logical change, at most about 200 changed lines, message format `type(scope): summary` (types: `feat`, `fix`, `test`, `refactor`, `chore`, `docs`).
- Run `npm run lint`, `npm run typecheck` and `npm test` before each commit; all must pass.
- Commit the test with the code it covers. Never commit generated secrets or `.env` files.

## Required unit tests (Vitest)
Write the test first for these functions; each needs the cases listed:
- `parseImport` (`src/lib/parse-import.ts`): all 22 examples of spec section 5.3, 500-row limit, 501-row error, 300 and 301 character lines, CSV with BOM and CRLF.
- `computeStats` (`src/lib/stats.ts`): empty library, 1 book, ties in top lists, rounding of percentages, all genres untagged.
- `normalizeTitle`, `normalizeAuthor`, `authorsMatch`, `titlesEqual`, `isDuplicate`, `jaccard`.
- The confidence rule (`classifyMatch`): matched, uncertain, not found, ambiguous title without author.
- `placeholderSpec` and `PlaceholderCover`: determinism and snapshot of 10 inputs.
- The LLM output validator: each of the 5 rejection rules in spec section 8.5.
- `sanitizeTitleForPrompt`, `inputHash` (key order independent), the rate-limit helper, and the theme contract tests.

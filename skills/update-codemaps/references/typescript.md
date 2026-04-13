# TypeScript/JavaScript Codemap Guidance

## Discovery Tools

- `tree -L 3 -I node_modules src/` for directory structure (always available)
- Read `package.json` for dependencies, scripts, and entry points
- Read `tsconfig.json` for path aliases and project references
- **Optional** (skip if not installed, never install): `npx ts-morph`, `npx madge`, `npx jsdoc2md`
- **Never run** `npx madge --image` — it writes files to the repo

## What to Capture

### Module Map
- Entry points: `app/`, `pages/`, `src/index.ts`, `server.ts`
- Route definitions (Next.js App Router, Express, Fastify)
- Middleware chains and plugin registration order
- Re-export barrels (`index.ts` files) and their public APIs

### Framework Patterns
- **Next.js**: App Router vs Pages Router, API routes, server actions, middleware.ts
- **React**: Component hierarchy, context providers, custom hooks
- **Node.js**: Service classes, repository pattern, dependency injection
- **Monorepo**: Workspace layout (turborepo/nx/pnpm workspaces), shared packages

### Data Layer
- ORM models (Prisma schema, Drizzle tables, TypeORM entities)
- Database migrations directory
- API client wrappers and SDK integrations
- State management (Redux slices, Zustand stores, React Query keys)

### Build & Config
- `tsconfig.json` path aliases and composite project references
- Bundle entry points (webpack/vite/esbuild config)
- Environment variable schema (`.env.example`, `zod` env validation)

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `frontend.md` | React/Vue/Svelte app with component tree |
| `backend.md` | API routes, services, middleware |
| `data.md` | Database schema, ORM models, migrations |
| `integrations.md` | External APIs, SDKs, third-party services |
| `workers.md` | Background jobs, queues, cron tasks |

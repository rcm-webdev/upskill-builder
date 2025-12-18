# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

```bash
# Install dependencies
bun install

# Run both server and client concurrently (main dev command)
bun run index.ts

# Format code with Prettier
bun run format
```

### Client (packages/client/)
```bash
bun run dev       # Start Vite dev server
bun run build     # TypeScript + Vite production build
bun run lint      # Run ESLint
```

### Server (packages/server/)
```bash
bun run dev       # Run with --watch for auto-reload
bun run start     # Run once without watch
```

## Architecture

This is a **Bun monorepo** with two packages:

```
packages/
├── client/   # React 19 + Vite + Tailwind CSS + shadcn/ui
└── server/   # Express 5 + OpenAI SDK
```

### Frontend-Backend Communication
- Vite proxies `/api/*` requests to `http://localhost:2121`
- Client runs on Vite's default port (5173)
- Server runs on port 2121

### Tech Stack
- **Runtime:** Bun (prefer Bun APIs over Node.js alternatives)
- **Frontend:** React 19, TypeScript, Vite, Tailwind CSS 4, shadcn/ui (New York style)
- **Backend:** Express 5, OpenAI SDK, dotenv
- **Code Quality:** Prettier, ESLint, Husky pre-commit hooks with lint-staged

### Component Patterns
- shadcn/ui components in `packages/client/src/components/ui/`
- Use `cn()` utility from `lib/utils.ts` for Tailwind class merging
- CVA (class-variance-authority) for component variants

## Environment Setup

Copy `packages/server/.env.example` to `.env` and configure:
- `PORT` - Server port (default: 2121)
- `OPENAI_API_KEY` - Required for LLM features

## Code Style

- Prettier config: single quotes, semicolons, trailing commas (ES5), 80 char width, 3-space tabs
- Import aliases: `@/*` maps to `src/*` in the client

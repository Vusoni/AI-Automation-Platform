# AI Automation Platform

A Next.js application for building and running automated workflows with AI providers (OpenAI, Anthropic, Gemini), integrations (Discord, Slack, HTTP), and background execution via Inngest.

## Tech Stack

- **Framework:** Next.js 15 (App Router, Turbopack)
- **Database:** PostgreSQL with Prisma
- **API:** tRPC with TanStack Query
- **Auth:** Better Auth (Polar)
- **Background jobs:** Inngest
- **AI:** Vercel AI SDK (OpenAI, Anthropic, Google Gemini)
- **Workflow editor:** React Flow (@xyflow/react)
- **Error tracking:** Sentry
- **Styling:** Tailwind CSS 4, Radix UI

## Features

- **Workflows** – Visual editor to create workflows with nodes (triggers, AI, HTTP, Discord, Slack, etc.)
- **Executions** – Run and inspect workflow runs with status and error details
- **Credentials** – Store API keys per type (OpenAI, Anthropic, Gemini)
- **Auth** – Login and signup with session management

## Prerequisites

- Node.js 20+
- PostgreSQL
- [Inngest CLI](https://www.inngest.com/docs/local-development) (for local background jobs)

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Environment variables

Copy `.env.example` to `.env` and set:

- `DATABASE_URL` – PostgreSQL connection string
- Auth and provider keys as needed (e.g. Polar, OpenAI, Anthropic, Gemini)
- Sentry DSN (optional, for error tracking)

### 3. Database

```bash
npx prisma generate
npx prisma db push
# or: npx prisma migrate dev
```

### 4. Run the app

**Development (Next.js only):**

```bash
npm run dev
```

**Development (Next.js + Inngest):**

```bash
npm run inngest:dev
# In another terminal:
npm run dev
```

**All-in-one (Next.js + Inngest via mprocs):**

```bash
npm run dev:all
```

Open [http://localhost:3000](http://localhost:3000). The app redirects to `/workflows` by default.

## Scripts

| Script        | Description                    |
|---------------|--------------------------------|
| `npm run dev` | Start Next.js dev (Turbopack)  |
| `npm run build` | Build for production        |
| `npm run start` | Start production server     |
| `npm run lint` | Run Biome check              |
| `npm run format` | Format with Biome          |
| `npm run inngest:dev` | Inngest dev server    |
| `npm run dev:all` | Next.js + Inngest (mprocs) |

## Project Structure

```
src/
├── app/
│   ├── (auth)/          # Login, signup
│   ├── (dashboard)/     # Workflows, executions, credentials
│   │   ├── (editor)/    # Workflow canvas (React Flow)
│   │   └── (rest)/      # List/detail pages
│   └── api/             # API routes, webhooks, tRPC, Inngest
├── components/          # Shared UI (sidebar, etc.)
├── features/            # Auth, credentials, workflows, executions, triggers
├── generated/           # Prisma client
├── lib/                 # Auth, Polar, utilities
└── trpc/                # tRPC routers
prisma/
└── schema.prisma        # Models: User, Workflow, Node, Connection, Execution, Credential
```

## Docs

- [Git branch workflow](docs/GIT_BRANCHES_GUIDE.md)

## License

Private.

# Project Setup Guide

This is a Next.js AI agent project built with Vercel AI SDK, Composio, Supermemory, and Telegram.

---

## Prerequisites

| Tool | Version | Check |
|------|---------|-------|
| Node.js | v18+ | `node --version` |
| pnpm | v10+ | `pnpm --version` |

### Install pnpm (if not installed)
```powershell
npm install -g pnpm
```
> After installing, close and reopen your terminal so pnpm is recognized.

---

## First-Time Setup

### 1. Install dependencies
```powershell
pnpm install
```

### 2. Configure environment variables

Create a `.env.local` file in the project root (copy from `.env.example`).

**Minimum required to run the app:**

| Variable | How to get |
|----------|-----------|
| `AUTH_SECRET` | Run: `node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"` |
| `POSTGRES_URL` | Create free DB at [neon.tech](https://neon.tech) → copy the pooled connection string |
| `AI_GATEWAY_API_KEY` | Sign up at [vercel.com/ai-gateway](https://vercel.com/ai-gateway) — $5 free credits |

**Optional (for advanced features):**

| Variable | Feature | How to get |
|----------|---------|-----------|
| `COMPOSIO_API_KEY` | Gmail, Slack, Notion tools | [dashboard.composio.dev](https://dashboard.composio.dev) → API Keys |
| `SUPERMEMORY_API_KEY` | Long-term memory | [supermemory.ai](https://supermemory.ai) → API Keys (free tier) |
| `TELEGRAM_BOT_TOKEN` | Telegram bot | [@BotFather](https://t.me/BotFather) → `/newbot` |
| `TELEGRAM_BOT_USERNAME` | Telegram bot | Same as above |
| `TELEGRAM_WEBHOOK_SECRET` | Telegram security | Any random string |
| `CRON_SECRET` | Scheduled tasks | Run: `node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"` |
| `BLOB_READ_WRITE_TOKEN` | File uploads | Vercel Dashboard → Storage → Blob |
| `REDIS_URL` | Rate limiting / resumable streams | Vercel Dashboard → Storage → Upstash |

### 3. Create the Neon Postgres database

1. Go to [neon.tech](https://neon.tech) and sign up (free)
2. Click **New Project** → name it → pick a region → **Create Project**
3. In the dashboard: **Connection Details** → select **Pooled connection** → copy the string
4. Paste it as `POSTGRES_URL` in `.env.local`

The connection string looks like:
```
postgresql://user:password@ep-xxx.us-east-1.aws.neon.tech/neondb?sslmode=require
```

### 4. Run database migrations
```powershell
npm run db:migrate
```
> Run this once on first setup, and again after any schema changes.

### 5. Start the development server
```powershell
npm run dev
```

App runs at **http://localhost:3000**

---

## Daily Development Commands

```powershell
# Start dev server
npm run dev

# Run database migrations (after schema changes)
npm run db:migrate

# Open Drizzle Studio (visual DB browser)
npm run db:studio

# Type check + lint
npm run check

# Auto-fix lint issues
npm run fix
```

---

## Windows-Specific Notes

- **`openssl` not available** — use Node.js instead to generate secrets:
  ```powershell
  node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
  ```

- **`pnpm` not found after install** — close and reopen PowerShell, or use `npm run <script>` as a fallback (all scripts in `package.json` work with `npm run` too).

- **pnpm full path** (if needed):
  ```
  C:\Users\<YourUser>\AppData\Roaming\npm\pnpm.cmd
  ```

---

## Project Structure

```
├── app/                  # Next.js App Router pages and API routes
│   ├── (chat)/           # Chat UI and main agent API route
│   └── api/              # Telegram webhook, cron tick, schedules
├── lib/
│   ├── ai/               # Models, prompts, tools
│   ├── db/               # Drizzle schema, queries, migrations
│   └── telegram.ts       # Telegram Bot API client
├── components/           # React UI components
├── .env.local            # Your local environment variables (DO NOT commit)
├── .env.example          # Template for env vars
└── SETUP.md              # This file
```

---

## Environment Variables Checklist

Before running, make sure these are filled in `.env.local`:

- [ ] `AUTH_SECRET` — required
- [ ] `POSTGRES_URL` — required
- [ ] `AI_GATEWAY_API_KEY` — required (for non-Vercel deploys)
- [ ] `COMPOSIO_API_KEY` — optional (enables external app tools)
- [ ] `SUPERMEMORY_API_KEY` — optional (enables memory)
- [ ] `TELEGRAM_BOT_TOKEN` — optional (enables Telegram)
- [ ] `CRON_SECRET` — optional (enables scheduled tasks)

---

## Deploying to Production

```powershell
vercel deploy --prod
```

After deploy, set all env vars in **Vercel Dashboard → Project → Settings → Environment Variables**, then re-register the Telegram webhook from `https://<your-domain>/telegram`.

See [README.md](README.md) for full deployment checklist.

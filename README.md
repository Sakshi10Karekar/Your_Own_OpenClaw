<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/4f69307a-50c8-4e79-aef3-c195006952d1" />

# General Purpose AI Agent Quickstart

A full-stack AI agent starter built with **Next.js**, **Vercel AI SDK**, **Composio**, and **Supermemory** — chat with an agent that can control Gmail, Slack, Notion, Calendar, and 1,000+ tools, remember facts across sessions, and be reached via web or Telegram.

## What's Inside

- **Chat UI** — Next.js 16 app with streaming responses and artifact rendering (code, documents, spreadsheets)
- **Tool Use** — Composio integration gives the agent one-click OAuth access to Gmail, Slack, Notion, Google Calendar, and 1,000+ apps
- **Long-term Memory** — Supermemory wraps the LLM so the agent remembers user facts across all sessions and channels
- **Telegram Bot** — same agent, accessible via Telegram with account linking
- **Scheduled Tasks** — agent-created cron jobs via Vercel Cron
- **Multi-model** — routes to any model (OpenAI, Anthropic, Google, xAI) via Vercel AI Gateway
- **Auth** — Auth.js with Neon Postgres for user management

## Tech Stack

| Layer | Tech |
|---|---|
| Framework | Next.js 16 + React 19 |
| AI | Vercel AI SDK + Vercel AI Gateway |
| Tools | Composio |
| Memory | Supermemory |
| Database | Neon Postgres + Drizzle ORM |
| Storage | Vercel Blob |
| Messaging | Telegram Bot API |
| Auth | Auth.js (next-auth v5) |


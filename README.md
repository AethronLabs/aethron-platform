<div align="center">

# ÆTHRON

### Turn any OpenAPI spec into a fully published, installable CLI — automatically.

Upload a spec. Generate commands. Ship a CLI to GitHub in minutes.

<br/>

https://pub-791252e542b34b9b85d72f368c5c362f.r2.dev/root-layer1.mp4

<br/>

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](./LICENSE)
[![Backend](https://img.shields.io/badge/backend-Rust-orange)](https://github.com/AethronLabs/aethron-backend)
[![App](https://img.shields.io/badge/app-Expo%20%2F%20React%20Native-blueviolet)](https://github.com/AethronLabs/aethron-app)

</div>

---

## What is Aethron?

Aethron takes your OpenAPI spec and does all the work of building and shipping a CLI for it:

1. **Upload** your OpenAPI spec to a project
2. **Generate** — AI reads your spec and produces named CLI commands with flags and descriptions
3. **Review** — tweak command names, flags, and descriptions before generating code
4. **Codegen** — Aethron generates Rust CLI source code from those commands
5. **Preview** the generated source before committing to publish
6. **Publish** — Aethron creates a GitHub repo, triggers a build, and publishes binaries for Linux, macOS, and Windows
7. **Install** — users install your CLI from the generated install URL

No boilerplate. No manual CLI wiring. Just a spec in and a working CLI out.

---

## Features

- **AI-powered command generation** — OpenAI reads your spec and names your commands intelligently
- **Full Rust CLI codegen** — generates idiomatic, production-ready Rust source using Clap
- **Multi-platform releases** — GitHub Actions builds binaries for Linux, macOS, and Windows automatically
- **Live sandbox** — spin up a Docker container and test your generated CLI in a live terminal over WebSocket before publishing
- **SSE build status** — real-time build progress streamed to the UI
- **Swagger UI** — full interactive API docs at `/swagger-ui`
- **JWT auth** — Supabase-backed authentication
- **Self-hostable** — one `docker compose up` and the full stack is running

---

## Demo

https://pub-791252e542b34b9b85d72f368c5c362f.r2.dev/root-layer1.mp4

---

## Quick Start

**Requirements:** Docker + Docker Compose

```bash
git clone --recurse-submodules https://github.com/AethronLabs/aethron-platform.git
cd aethron-platform
cp .env.example .env
# fill in .env — see Environment Variables below
docker compose up --build
```

| Service | URL |
|---------|-----|
| Web app | http://localhost:8080 |
| API | http://localhost:3000 |
| Swagger UI | http://localhost:3000/swagger-ui |

---

## Environment Variables

Copy `.env.example` → `.env` and fill in all values.

| Variable | Where to get it |
|----------|----------------|
| `POSTGRES_PASSWORD` | Set any strong password |
| `JWT_SECRET` | Any long random string |
| `SUPABASE_URL` | Supabase dashboard → Project Settings → API |
| `SUPABASE_JWT_SECRET` | Supabase dashboard → Project Settings → API |
| `OPENAI_API_KEY` | platform.openai.com/api-keys |
| `GITHUB_TOKEN` | GitHub → Settings → Developer Settings → PAT (repo + org scope) |
| `GITHUB_ORG` | GitHub org where generated CLI repos will be created |
| `GITHUB_WEBHOOK_SECRET` | Any random string — set same value in your GitHub org webhook |
| `R2_BUCKET` / `R2_ACCOUNT_ID` / `R2_ACCESS_KEY_ID` / `R2_SECRET_ACCESS_KEY` | Cloudflare dashboard → R2 |
| `BASE_URL` | Public URL of this API (e.g. `https://api.yourdomain.com`) |
| `EXPO_PUBLIC_SUPABASE_URL` | Same as `SUPABASE_URL` |
| `EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | Supabase dashboard → Project Settings → API → Publishable key |
| `EXPO_PUBLIC_API_URL` | URL of the backend (e.g. `http://localhost:3000`) |

---

## Architecture

```
┌──────────────────────┐         ┌────────────────────────┐
│     aethron-app      │  HTTP   │    aethron-backend     │
│  (nginx · port 8080) │ ──────▶ │    (Axum · port 3000)  │
└──────────────────────┘         └────────────┬───────────┘
                                               │
                                  ┌────────────▼───────────┐
                                  │       PostgreSQL        │
                                  └────────────────────────┘
                                               │
                              ┌────────────────┼──────────────────┐
                              │                │                  │
                    ┌─────────▼──────┐  ┌──────▼──────┐  ┌───────▼──────┐
                    │   OpenAI API   │  │   GitHub    │  │      R2      │
                    │  (codegen/AI)  │  │ (releases)  │  │  (binaries)  │
                    └────────────────┘  └─────────────┘  └──────────────┘
```

---

## Stack

| Layer | Tech |
|-------|------|
| API | Rust · Axum · SQLx · Tokio |
| Database | PostgreSQL |
| Auth | Supabase JWT |
| AI | OpenAI API |
| Storage | Cloudflare R2 |
| Publishing | GitHub API + Actions |
| Sandbox | Docker + WebSocket terminal |
| Frontend | React Native · Expo · React Navigation |

---

## Repos

| Repo | Description |
|------|-------------|
| [aethron-backend](https://github.com/AethronLabs/aethron-backend) | Rust API — auth, codegen, sandbox, publishing |
| [aethron-app](https://github.com/AethronLabs/aethron-app) | React Native (Expo) — web + mobile frontend |
| [aethron-platform](https://github.com/AethronLabs/aethron-platform) | Umbrella repo — Docker Compose self-hosting |

---

## Mobile

The Expo app runs on iOS and Android too. For mobile development:

```bash
cd aethron-app
npm install
cp .env.example .env  # set EXPO_PUBLIC_API_URL to your backend
npx expo start
```

---

## Contributing

Contributions go to the individual repos:

- Backend changes → [aethron-backend](https://github.com/AethronLabs/aethron-backend)
- Frontend changes → [aethron-app](https://github.com/AethronLabs/aethron-app)
- Docker / deployment → this repo

Open an issue before starting large changes.

---

## Updating submodules

```bash
git submodule update --remote --merge
git add aethron-backend aethron-app
git commit -m "chore: update submodules"
```

---

## License

Apache License 2.0 — see [LICENSE](./LICENSE).

# Aethron Platform

One-command self-hosted deployment of the full Aethron stack — backend API + web app.

> Turn any OpenAPI spec into a fully published, installable CLI — automatically.

## Repos

| Repo | Description |
|------|-------------|
| [aethron-backend](https://github.com/AethronLabs/aethron-backend) | Rust API — codegen, publishing, sandbox |
| [aethron-app](https://github.com/AethronLabs/aethron-app) | React Native (Expo) — web + mobile frontend |

## Quick start

**Requirements:** Docker + Docker Compose

```bash
git clone --recurse-submodules https://github.com/AethronLabs/aethron-platform.git
cd aethron-platform
cp .env.example .env
# fill in .env with your credentials
docker compose up --build
```

| Service | URL |
|---------|-----|
| Web app | http://localhost:8080 |
| API | http://localhost:3000 |
| Swagger UI | http://localhost:3000/swagger-ui |

## Environment variables

Copy `.env.example` to `.env` and fill in all values. See comments in the file for where to get each key.

Required external services:
- **Supabase** — auth (free tier works)
- **OpenAI** — CLI command + code generation
- **GitHub** — repo creation + release publishing (PAT with `repo` + `org` scope)
- **Cloudflare R2** — binary + source storage (S3-compatible, free tier works)

## Architecture

```
┌─────────────┐     HTTP      ┌─────────────────┐
│  aethron-app│ ──────────── ▶│ aethron-backend │
│  (nginx:8080│               │   (Axum:3000)   │
└─────────────┘               └────────┬────────┘
                                        │
                               ┌────────▼────────┐
                               │   PostgreSQL    │
                               └─────────────────┘
```

The app is served as a static web build. For mobile (iOS/Android), run the Expo dev server directly from the `aethron-app` repo.

## Updating submodules

```bash
git submodule update --remote --merge
git add aethron-backend aethron-app
git commit -m "chore: update submodules"
```

## Contributing

Contributions go to the individual repos:
- Backend changes → [aethron-backend](https://github.com/AethronLabs/aethron-backend)
- Frontend changes → [aethron-app](https://github.com/AethronLabs/aethron-app)
- Docker / deployment changes → this repo

## License

Apache License 2.0 — see [LICENSE](./LICENSE).

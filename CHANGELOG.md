# Changelog

All notable changes to Aethron will be documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

### Added
- Community health files: `CONTRIBUTING.md`, `SECURITY.md`, issue/PR templates
- CI workflow to validate docker-compose on every push
- Healthcheck on backend service — app waits for backend readiness before starting
- Platform support matrix documenting macOS / Linux / Windows Docker behavior
- `R2_PUBLIC_URL` env var — self-hosters can now point to their own R2 bucket

### Fixed
- Removed hardcoded Cloudflare R2 CDN URL from backend source
- Removed debug `console.log` statements (including partial token logging) from frontend
- Fixed architecture diagram — now correctly shows Supabase instead of standalone PostgreSQL
- Fixed env docs — replaced stale `POSTGRES_PASSWORD` with `DATABASE_URL`

---

## [0.1.0-alpha] — Initial public release

### Added
- Upload OpenAPI spec → AI generates named CLI commands
- Review and edit commands before code generation
- Full Rust CLI codegen using Clap
- GitHub repo creation + Actions pipeline for multi-platform binary releases (Linux, macOS, Windows)
- Live sandbox — spin up a Docker container and test your CLI over WebSocket before publishing
- SSE real-time build status streaming
- Supabase JWT authentication
- Swagger UI at `/swagger-ui`
- Self-hostable via `docker compose up --build`

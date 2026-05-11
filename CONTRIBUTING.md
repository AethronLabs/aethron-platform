# Contributing to Aethron

## Where to contribute

Changes go to the individual repos:

| Area | Repo |
|------|------|
| Backend (Rust API) | [aethron-backend](https://github.com/AethronLabs/aethron-backend) |
| Frontend (Expo app) | [aethron-app](https://github.com/AethronLabs/aethron-app) |
| Docker / deployment | this repo |

Open an issue before starting large changes.

---

## Local setup

```bash
git clone --recurse-submodules https://github.com/AethronLabs/aethron-platform.git
cd aethron-platform
cp .env.example .env
# fill in .env — all variables are required
docker compose up --build
```

| Service | URL |
|---------|-----|
| Web app | http://localhost:8080 |
| API | http://localhost:3000 |
| Swagger UI | http://localhost:3000/swagger-ui |

---

## Testing the sandbox locally

The sandbox feature requires Docker socket access:

```bash
# Verify Docker is running
docker info

# Build the sandbox image (required for sandbox to work)
cd aethron-backend
docker build -t aethron-sandbox:latest -f sandbox.Dockerfile .

# Start the stack
cd ..
docker compose up --build
```

Then use the UI to start a sandbox session — it will spin up a container on your local Docker daemon.

---

## Coding standards

**Backend (Rust):**
- Run `cargo fmt` before committing
- Run `cargo clippy` and fix all warnings
- Use `AppError` for all error returns — no `.unwrap()` in route handlers

**Frontend (JS/React Native):**
- No `console.log` in committed code
- Keep API calls in `src/utils/api.js` — don't call `fetch` directly in components

---

## Branch naming

```
feat/short-description
fix/short-description
chore/short-description
docs/short-description
```

---

## Submodules

Changes to backend or frontend must be committed inside the submodule first, then the pointer updated in this repo.

```bash
cd aethron-backend   # or aethron-app
git add .
git commit -m "feat: your change"
git push

cd ..
git add aethron-backend
git commit -m "chore: update submodule"
git push
```

---

## Pull requests

- One thing per PR — keep scope tight
- No secrets or API keys in diffs
- Test with `docker compose up --build` before submitting
- Reference the issue number in the PR description (`Closes #123`)

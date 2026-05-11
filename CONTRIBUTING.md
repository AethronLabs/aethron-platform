# Contributing to Aethron

## Where to contribute

Changes go to the individual repos:

| Area | Repo |
|------|------|
| Backend (Rust API) | [aethron-backend](https://github.com/AethronLabs/aethron-backend) |
| Frontend (Expo app) | [aethron-app](https://github.com/AethronLabs/aethron-app) |
| Docker / deployment | this repo |

Open an issue before starting large changes.

## Local setup

```bash
git clone --recurse-submodules https://github.com/AethronLabs/aethron-platform.git
cd aethron-platform
cp .env.example .env
# fill in .env
docker compose up --build
```

## Submodules

This repo uses git submodules. Changes to backend or frontend must be committed inside the submodule first, then the pointer updated here.

```bash
cd aethron-backend   # or aethron-app
git add .
git commit -m "your change"
git push
cd ..
git add aethron-backend
git commit -m "chore: update submodule"
```

## Pull requests

- Keep PRs focused — one thing per PR
- No secrets or API keys in diffs
- Test with `docker compose up --build` before submitting

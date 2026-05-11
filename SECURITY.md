# Security Policy

## Reporting a vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

Email: vanshsoniofficial@gmail.com

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Any suggested fix (optional)

You'll get a response within 72 hours. Please allow time to patch before public disclosure.

## Scope

This covers the `aethron-platform` deployment stack and its submodules (`aethron-backend`, `aethron-app`).

## Security notes for self-hosters

- Never commit your `.env` file — it contains live API keys
- The sandbox feature mounts the Docker socket — run on a trusted machine only
- Rotate all credentials if you suspect exposure
- Keep Docker and dependencies up to date

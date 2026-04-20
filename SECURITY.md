# Security notes

## What's safe to commit (and already is)

- **Affiliate IDs** (`Allianceid`, `SID`, `trip_sub1`, `trip_sub3`) — public by design. They ride in every outbound URL a user clicks. Forking this repo and replacing them with your own IDs is the whole point.
- **Free API endpoints with no auth** — Open-Meteo, ipapi.co. No keys, no risk.

## What must NEVER be committed

- **Notion integration tokens** (`secret_...` — API keys to your Notion workspace)
- **GitHub Personal Access Tokens** (used by CI or local tools)
- **`.env` files** of any kind
- **Private API keys** — OpenAI, Anthropic, Google Cloud, AWS, Stripe, etc.
- **Database credentials** or connection strings containing passwords
- **Session/JWT signing secrets**

The `.gitignore` at the repo root blocks all the common patterns (`.env`, `*.key`, `secrets.json`, etc.) but **git only protects you from files it doesn't yet track** — if you accidentally `git add secret.json` before gitignoring it, the file ends up in history forever.

## If you ever leak a secret by accident

1. **Rotate the secret immediately** — change the password / regenerate the API key on the provider's side. Revoking is always faster than scrubbing git history.
2. Then (optionally) rewrite history with `git filter-repo` or BFG Repo-Cleaner to remove the file from past commits.
3. `git push --force` to overwrite the remote.

But step 1 is what actually protects you. Steps 2–3 only stop future observers; the leak already happened, and the old key must be assumed compromised.

## Reporting

Found a security issue in this repo? Open a private security advisory via GitHub's Security tab (not a public issue).

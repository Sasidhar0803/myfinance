# MyFinance

Local-first personal finance tracker. Everything runs in your browser; there is no backend.

## Run locally
    npm install
    npm run dev      # http://localhost:5173
    npm test         # unit tests (calculations + encryption)
    npm run build

## Deploy to GitHub Pages
1. Push to a GitHub repo with a `main` branch.
2. Repo → Settings → Pages → Source: **GitHub Actions**.
3. Every push to `main` runs tests, builds with base path `/<repo-name>/`, and deploys.

## Where your data lives
In your browser's IndexedDB (`myfinance` → `kv`), as one AES-256-GCM encrypted blob. The key is derived from your passphrase with PBKDF2-SHA256 (310,000 iterations) and a random salt; each save uses a fresh nonce. The passphrase is never stored. No data leaves your device and there is no analytics (the only external request is the Google Fonts stylesheet).

## Backup and recovery
Settings → Download encrypted backup saves `{salt, vault}` as JSON. Keep it and your passphrase safe. **A lost passphrase cannot be recovered.** Clearing site data deletes your vault, so back up regularly.

## Known limitations
- Browser storage can be cleared by the browser or OS; it is not a substitute for backups.
- Anyone with your passphrase and access to your unlocked browser session can read your data. Sessions auto-lock after 5 minutes idle.
- Implemented: lock screen, overview dashboard, transactions (income, expense, refund, transfer), accounts, encrypted backup download, erase.
- Not yet implemented: budgets, savings goals, investments, recurring payments, net-worth history, analytics, health score, planners, calendar, CSV/XLSX/PDF import and export, backup restore, custom categories, settings for currency/date/financial year, demo data.

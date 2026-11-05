# Winprizez

Spin wheel site. Everything on Cloudflare (Pages for the site, Workers and D1 for the backend later).

## Structure

```
Winprizez/
├── .github/workflows/
│   └── deploy-pages.yml     # manual deploy of the site to Cloudflare Pages
└── hosting/
    └── assets/
        └── index.html       # the whole front page (wheel, prizes, winners, wallet)
```

The Worker (`src/`, `wrangler.toml`), the D1 `schema.sql` and a
`deploy-worker.yml` will be added alongside these in the next steps,
the same way as the KavoPay repo.

## Setup (once)

In the repo go to Settings, Secrets and variables, Actions, and add:

- `CLOUDFLARE_API_TOKEN` (needs the Cloudflare Pages Edit permission)
- `CLOUDFLARE_ACCOUNT_ID`

Use the same values as the KavoPay repo. Secrets are per repo, so they
must be added here too.

## Deploying

Actions tab, then **Deploy Winprizez Web Pages**, then **Run workflow**.

It creates the Pages project `winprizez` if it does not exist yet, then
deploys `hosting/assets`. The dev link will be:

```
https://winprizez.pages.dev
```

If that name is already taken on Cloudflare, change `winprizez` to
another name in the two `command:` lines of `deploy-pages.yml`.

## Demo mode

At the top of the script in `index.html`, `var API = '';` means the page
runs on built-in sample prizes and picks results in the browser. That is
only for previewing the design. When the Worker is ready, set it to
`'/api'` so the server decides every spin and the admin controls the
spin price and the prizes.

## Note

This repo is public. Never commit keys, tokens or passwords. They belong
in GitHub Secrets and Cloudflare Worker secrets only.

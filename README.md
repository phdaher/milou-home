# Milou Home

Static website for [milouhome.com](https://milouhome.com), hosted on Cloudflare Workers (static assets).

## Project structure

```
public/            Everything here is uploaded as-is
  index.html       The site (single page)
  _headers         Cache and security headers
  img/             Product and section photos
  *.png            Logos, favicon, emblem
wrangler.jsonc     Cloudflare Worker configuration
```

There is no build step: what's in `public/` is what gets served.

## Prerequisites

- [Node.js](https://nodejs.org/) 18 or later (for `npx`)
- Access to the Cloudflare account that owns the `milouhome.com` zone

## Run locally

```sh
npx wrangler dev
```

Then open http://localhost:8787. Edits to files in `public/` show up on reload.

You can also open `public/index.html` directly in a browser for quick checks.

## Deploy

1. Log in to Cloudflare (first time only; opens a browser):

   ```sh
   npx wrangler login
   ```

   Confirm you're on the right account with `npx wrangler whoami`.

2. Deploy:

   ```sh
   npx wrangler deploy
   ```

   This uploads `public/` to the `milou-home` Worker and attaches it to the custom domains `milouhome.com` and `www.milouhome.com`. Only changed files are uploaded.

3. Check https://milouhome.com. Static files are cached by browsers for up to 7 days (see `public/_headers`), so use a hard refresh or a private window to see image changes.

### Notes

- The `workers.dev` subdomain and preview URLs are disabled, so the custom domains are the only way to reach the site.
- The custom domains are created automatically on the first deploy; the `milouhome.com` zone must already be on the same Cloudflare account.
- To roll back, use `npx wrangler rollback` or pick an earlier version under **Workers & Pages → milou-home → Deployments** in the Cloudflare dashboard.

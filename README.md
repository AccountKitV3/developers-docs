# Account Kit API Documentation

Swagger UI documentation for the Account Kit API, hosted at [developers.account-kit.com](https://developers.account-kit.com).

## Structure

```
.
├── index.html        # Swagger UI entry point
├── openapi.yaml      # OpenAPI 3.1 specification
├── CNAME             # Custom domain for GitHub Pages
└── .github/
    └── workflows/
        └── pages.yml # GitHub Actions deployment workflow
```

## Local development

Open `index.html` with a local HTTP server — the Swagger UI loads `openapi.yaml` via a relative fetch, so a plain `file://` URL will fail due to browser CORS restrictions.

```bash
# Python
python3 -m http.server 8080

# Node (npx)
npx serve .
```

Then visit `http://localhost:8080`.

## Editing the spec

Update `openapi.yaml` following the [OpenAPI 3.1 specification](https://spec.openapis.org/oas/v3.1.0). Changes pushed to `main` are automatically deployed via GitHub Actions.

## Deployment

### 1. Create and push the GitHub repo

```bash
gh repo create account-kit/developers-docs --public
git remote add origin https://github.com/account-kit/developers-docs.git
git push -u origin main
```

### 2. Enable GitHub Pages

In the GitHub repo: **Settings → Pages → Source**, set to **GitHub Actions**. The workflow in `.github/workflows/pages.yml` handles deployment on every push to `main`.

### 3. Configure DNS (Cloudflare)

`account-kit.com` is hosted on Cloudflare (`stella.ns.cloudflare.com` / `dakota.ns.cloudflare.com`).

In the Cloudflare dashboard for the `account-kit.com` zone, add a CNAME record:

| Type  | Name         | Target                       | Proxy status |
|-------|--------------|------------------------------|--------------|
| CNAME | developers   | account-kit.github.io        | DNS only (grey cloud) |

> **Important:** set the record to **DNS only** (grey cloud), not proxied. Cloudflare's proxy intercepts TLS and prevents GitHub Pages from provisioning its own HTTPS certificate. Once the cert is issued and the custom domain is verified in GitHub, you can optionally re-enable the proxy.

### 4. Confirm the custom domain in GitHub Pages

Back in **Settings → Pages**, set the custom domain to `developers.account-kit.com` and check **Enforce HTTPS** once the certificate has been issued (usually within a few minutes of the DNS record propagating).

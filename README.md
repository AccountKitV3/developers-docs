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

## Custom domain setup

The `CNAME` file points GitHub Pages to `developers.account-kit.com`. In your DNS provider, add a `CNAME` record:

```
developers.account-kit.com  →  <your-github-org>.github.io
```

Then in the GitHub repo settings under **Pages**, confirm the custom domain is set and HTTPS is enforced.

# AGENTS.md

This project is a single static HTML page (`index.html`) plus a `screenshots/` folder of images. No build step, no backend, no package manager, no external credentials.

## Running it

```
docker compose -f docker-compose.base44.yml up -d
```

Serves `index.html` on host port 3000 via `nginx:alpine`.

## Quirks

- The repo directory is permission `700` (root-only), so nginx's default non-root worker cannot read the bind-mounted files. A custom `nginx.conf` (mounted into the container) sets `user root;` so workers can traverse and serve the source. Keep that config file.
- The page is static; edits to `index.html` appear on browser refresh (no live-reload dev server). Call `reload_preview` after changes if you want the preview to refresh automatically.
- `index.html` references `screenshots/banner.jpg` and `screenshots/{1..70}.jpg`; missing images are silently removed client-side via `img.onerror`.

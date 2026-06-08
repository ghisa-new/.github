# GHISA

Multi-platform retail & e-commerce infrastructure.

## Repositories

| Repo | Description | Stack |
|------|-------------|-------|
| [app-gixa](https://github.com/ghisa-new/app-gixa) | E-commerce integration platform (NEBIM + Shopify + Trendyol) | Next.js, PostgreSQL, Drizzle |
| [app-gixa-vms](https://github.com/ghisa-new/app-gixa-vms) | Warehouse terminal app (transfers, put-away, pick, adjust) | Next.js, SQLite, NEBIM Integrator API |
| [app-mobile](https://github.com/ghisa-new/app-mobile) | Customer mobile app (iOS + Android) | React Native, Expo, Shopify Storefront API |
| [app-points-api](https://github.com/ghisa-new/app-points-api) | Loyalty points API | Python, FastAPI, NEBIM |
| [app-rfid](https://github.com/ghisa-new/app-rfid) | RFID inventory app for hand terminals | Kotlin, Android, Urovo SDK |
| [app-shopify-theme](https://github.com/ghisa-new/app-shopify-theme) | Shopify storefront theme | Liquid, JS, CSS |
| [mcp-fleet](https://github.com/ghisa-new/mcp-fleet) | MCP servers for AI agents (GitHub, Pixa, Shopify, Trendyol) | Node.js, TypeScript, Docker |

## Infrastructure

| Service | URL | Server |
|---------|-----|--------|
| VMS Warehouse App | https://vms.verioku.dev | 46.62.246.160 |
| MCP Fleet Docs | https://docs.verioku.dev | 46.62.246.160 |
| Gixa Panel | 46.62.245.28 | 46.62.245.28 |
| Image CDN | https://verioku.com | Cloudflare R2 |

## Servers

| IP | Role |
|----|------|
| 46.62.246.160 | MCP fleet + Apps (Docker) |
| 46.62.245.28 | Pixa/Gixa (Docker Compose) |

## Networking

- **Domain:** `verioku.dev` (Cloudflare Registrar)
- **CDN domain:** `verioku.com` (Cloudflare R2)
- **Tunnel:** Cloudflare Tunnel `ghisa-fleet` on 46.62.246.160 routes `*.verioku.dev` through Cloudflare without opening firewall ports
- **SSL:** Cloudflare handles HTTPS termination, origin serves HTTP

## Deployment

Apps and MCP servers deploy via GitHub Actions on push to `main`. Each repo has a `.github/workflows/deploy.yml`.

Required repo secrets: `SSH_PRIVATE_KEY` (Hetzner SSH key), `DEPLOY_HOST` (mcp-fleet only).

## Container Layout (46.62.246.160)

| Container | Port | Purpose |
|-----------|------|---------|
| app-gixa-vms | 3100 | Warehouse terminal app |
| mcp-fleet-docs | 3101 | Static docs site |
| pixa-mcp | 3203 | Pixa DB MCP |
| github-mcp-proxy | 3204 | GitHub API MCP |
| Caddy | 80 | Reverse proxy |
| cloudflared | - | Cloudflare Tunnel (outbound) |

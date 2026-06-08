# GHISA

Multi-platform retail & e-commerce infrastructure.

## Repositories

| Repo | Description | Stack | URL |
|------|-------------|-------|-----|
| [app-gixa](https://github.com/ghisa-new/app-gixa) | E-commerce integration platform (NEBIM + Shopify + Trendyol) | Next.js, PostgreSQL, Drizzle | https://gixa.verioku.dev |
| [app-gixa-vms](https://github.com/ghisa-new/app-gixa-vms) | Warehouse terminal app (transfers, put-away, pick, adjust) | Next.js, SQLite, NEBIM Integrator | https://vms.verioku.dev |
| [app-store](https://github.com/ghisa-new/app-store) | Store reporting dashboard (stats, notifications, operations) | Next.js, SQLite | https://store.verioku.dev |
| [app-mobile](https://github.com/ghisa-new/app-mobile) | Customer mobile app (iOS + Android) | React Native, Expo, Shopify Storefront | — |
| [app-points-api](https://github.com/ghisa-new/app-points-api) | Loyalty points API | Python, FastAPI, NEBIM | — |
| [app-rfid](https://github.com/ghisa-new/app-rfid) | RFID inventory app for hand terminals | Kotlin, Android, Urovo SDK | — |
| [app-shopify-theme](https://github.com/ghisa-new/app-shopify-theme) | Shopify storefront theme | Liquid, JS, CSS | — |
| [mcp-fleet](https://github.com/ghisa-new/mcp-fleet) | MCP servers for AI agents (GitHub, Pixa, Shopify, Trendyol) | Node.js, TypeScript, Docker | https://docs.verioku.dev |

## Infrastructure

| Service | URL | Port | Container |
|---------|-----|------|-----------|
| Gixa Panel | https://gixa.verioku.dev | 3102 | app-gixa |
| VMS Warehouse | https://vms.verioku.dev | 3100 | app-gixa-vms |
| Store Dashboard | https://store.verioku.dev | 3103 | app-store |
| MCP Docs | https://docs.verioku.dev | 3101 | mcp-fleet-docs |
| Image CDN | https://verioku.com | — | Cloudflare R2 |

## Servers

| IP | Role |
|----|------|
| 46.62.246.160 | Apps + MCP fleet (Docker) |
| 46.62.245.28 | Pixa production (Docker Compose) |

## Networking

- **Domain:** `verioku.dev` (Cloudflare Registrar)
- **CDN:** `verioku.com` (Cloudflare R2)
- **Tunnel:** Cloudflare Tunnel `ghisa-fleet` on 46.62.246.160
- **SSL:** Cloudflare handles HTTPS, origin serves HTTP
- **Reverse proxy:** Caddy routes subdomains to containers

## Deployment

GitHub Actions on push to `main`. Each repo has `.github/workflows/deploy.yml`.

Required secret: `SSH_PRIVATE_KEY` (Hetzner SSH key).

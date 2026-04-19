# go-cookbook

> Snippet-sized recipes for building production Go backends with Fiber — webhook idempotency, JWT, OAuth2, Stripe/payment integration, CSRF, rate limiting, file uploads, auth-jwt-postgres flows. Curated for commercial subscription and internal-tool use cases.

<p align="left">
  <img alt="Go" src="https://img.shields.io/badge/Go-1.22%2B-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img alt="Fiber" src="https://img.shields.io/badge/Fiber-v2%20%2F%20v3-00ADD8?style=flat-square">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-green?style=flat-square">
  <img alt="Maintained" src="https://img.shields.io/badge/Maintained%20by-Tunasoft%20Yazılım-181717?style=flat-square">
</p>

---

## What this is

`go-cookbook` is Tunasoft Yazılım's curated collection of minimal, runnable Go + Fiber recipes. Each recipe is a small self-contained project solving one concrete problem the way we do it in commercial delivery.

Think of it as the companion to [`clean-go-starter`](https://github.com/tunacosgun/clean-go-starter): when the template covers the skeleton, the cookbook shows the **how** for individual building blocks.

## Highlighted recipes

### Payment & webhook

| Recipe                                                    | What it shows                                           |
|-----------------------------------------------------------|---------------------------------------------------------|
| [`auth-jwt`](./auth-jwt/)                                 | JWT issuance & verification, rotating keys              |
| [`auth-docker-postgres-jwt`](./auth-docker-postgres-jwt/) | JWT with Postgres-backed user store, Docker Compose     |
| [`oauth2`](./oauth2/)                                     | OAuth2 authorization code flow with Fiber               |
| [`oauth2-google`](./oauth2-google/)                       | Google OAuth2 federation                                |
| [`jwt`](./jwt/)                                           | Minimal JWT bearer-token protected endpoint              |
| [`csrf`](./csrf/) + [`csrf-with-session`](./csrf-with-session/) | CSRF protection with and without session affinity |

### Data & persistence

| Recipe                               | What it shows                                      |
|--------------------------------------|----------------------------------------------------|
| [`gorm`](./gorm/)                    | GORM basics — migrations, CRUD, relations          |
| [`gorm-mysql`](./gorm-mysql/)        | GORM against MySQL with Docker                     |
| [`ent`](./ent/) + [`entgo-sveltekit`](./entgo-sveltekit/) | Facebook's Ent ORM, with and without a frontend |
| [`sqlc`](./sqlc/)                    | Typed SQL queries with sqlc                        |
| [`sqlboiler`](./sqlboiler/)          | SQLBoiler (Model → Go type) workflow               |

### Middleware & operational

| Recipe                                    | What it shows                                      |
|-------------------------------------------|----------------------------------------------------|
| [`rate-limiter`](./rate-limiter/)         | Rate limiting with the Fiber middleware            |
| [`monitoring-with-apitally`](./v2/monitoring-with-apitally/) | API observability with Apitally |
| [`prometheus`](./prometheus/) *(planned)* | Prometheus metrics middleware                      |
| [`graceful-shutdown`](./graceful-shutdown/) | SIGTERM handling and in-flight request drain    |

### External integrations

| Recipe                                    | What it shows                                      |
|-------------------------------------------|----------------------------------------------------|
| [`envoy-extauthz`](./envoy-extauthz/)     | Envoy external authorization filter                |
| [`clean-architecture`](./clean-architecture/) | Clean Architecture applied to a Fiber service |
| [`hexagonal`](./hexagonal/)               | Hexagonal architecture layout for Fiber            |

### Transport & response

| Recipe                                    | What it shows                                      |
|-------------------------------------------|----------------------------------------------------|
| [`websocket-chat`](./websocket-chat/)     | WebSocket chat server                              |
| [`sse`](./sse/) *(planned)*               | Server-Sent Events stream                          |
| [`rss-feed`](./rss-feed/)                 | RSS generation                                     |
| [`file-server`](./file-server/)           | Static file serving with range requests            |

*Full index of all recipes in [`./docs/INDEX.md`](./docs/INDEX.md).*

## Why we maintain this

The best way to onboard a team member or evaluate a library is not reading documentation — it's running a 40-line recipe and seeing how the pieces fit. We consult this cookbook **weekly** during commercial delivery: "how do we wire Stripe webhooks again? — check `go-cookbook/webhook`."

Each recipe is **complete and runnable**:

```bash
cd oauth2-google
go mod tidy
go run main.go
```

No hunting for a missing import or a deleted config step.

## How we use it

During a new engagement, we:

1. Pick the recipes that match the product's needs (webhook, JWT, payment gateway)
2. Copy the patterns into the project bootstrapped from [`clean-go-starter`](https://github.com/tunacosgun/clean-go-starter)
3. Adapt to the domain — wrap the HTTP boilerplate in our ports/adapters
4. Write domain tests on top

This keeps velocity high in the first week of a project.

## Related Tunasoft projects

- [`clean-go-starter`](https://github.com/tunacosgun/clean-go-starter) — the production template recipes drop into
- [`ddd-workout-kit`](https://github.com/tunacosgun/ddd-workout-kit) — full-stack DDD reference for complex domains
- [`identity-hub`](https://github.com/tunacosgun/identity-hub) — production auth server; see `auth-jwt` / `oauth2` recipes for the building blocks behind it

## Credits

Built on top of the excellent [`gofiber/recipes`](https://github.com/gofiber/recipes) — the canonical Fiber cookbook. This fork is maintained by Tunahan Coşgun and Duygu Durmuş at Tunasoft Yazılım and curated for commercial subscription and internal-tool use cases.

## License

MIT — see [`LICENSE`](./LICENSE).

## Contact

- 📧 [info@tunahancosgun.dev](mailto:info@tunahancosgun.dev)
- 🌐 [tunahancosgun.dev](https://tunahancosgun.dev)
- 📅 [Book a consultation](https://cal.com/tunacosgun/intro)

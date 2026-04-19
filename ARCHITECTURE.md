# Architecture of a cookbook recipe

Each recipe in `go-cookbook` follows a consistent shape so readers can skim them quickly. This doc describes the conventions we enforce on every recipe.

## Shape of a recipe

```
recipe-name/
├── README.md         # what it solves, how to run, key notes
├── go.mod            # independent module — no shared deps
├── main.go           # the runnable entry point
├── docker-compose.yml (optional) # if the recipe needs Postgres / Redis / etc.
├── migrations/ (optional) # SQL migrations if DB-backed
└── .env.example (optional) # any required env vars
```

### README template

Every recipe README follows the same four sections:

```markdown
## What this recipe does
One-paragraph description of the problem.

## Run it
Commands to clone, set up, and run.

## Key parts
Pointers to the 3-5 most important lines or functions in `main.go`.

## Caveats
Production hardening concerns the recipe does NOT cover.
```

The **Caveats** section matters — it is what separates a "demo" from a "template." A reader knows what they still need to add.

## Recipes we maintain as foundational

### `auth-jwt-postgres-docker`

The canonical "user registration + login + JWT-protected endpoint" recipe. Shows:

- Bcrypt password hashing with a sensible cost factor
- JWT HS256 signing with a rotatable secret
- Middleware that parses the JWT and injects the user into request context
- A protected endpoint that reads the user from context
- Docker Compose setup with Postgres + a migration runner

Caveats listed: no refresh tokens, no rate limiting on login, no OAuth; for production see [`identity-hub`](https://github.com/tunacosgun/identity-hub).

### `oauth2-google`

Google OAuth2 authorization code flow. Shows the full redirect-callback-exchange pattern with explicit CSRF state.

### `clean-architecture`

A minimum viable Clean Architecture layout in Fiber. Domain → use case → adapter layering, no shared mutable state, tests against mocked ports. Used as a teaching aid.

### `rate-limiter`

Demonstrates Fiber's built-in rate-limit middleware **and** a custom Redis-backed sliding-window implementation. The custom one is the pattern we use for distributed deployments.

## Recipes we extend vs. keep-as-upstream

| Category                         | Our approach                                    |
|----------------------------------|------------------------------------------------|
| Auth / JWT / OAuth2              | We extend with Postgres + structured logging   |
| Payment (webhook, Stripe)        | We add idempotency-key patterns                 |
| Database (gorm, sqlc, ent)       | Upstream is fine; we use as-is                 |
| Middleware (rate limit, CSRF)    | We document production caveats                  |
| Transport (WebSocket, SSE)       | Upstream is fine                               |
| Frontend integrations            | Upstream is fine                               |

## Recipe selection workflow

When starting a new commercial project, we sit down with the recipe index and tag which ones apply:

1. ✅ Will need auth → pull `auth-jwt-postgres-docker` pattern
2. ✅ Will accept payments → pull `webhook` + idempotency pattern
3. ✅ Will have admin endpoints → pull `rate-limiter` pattern
4. ❌ Not doing OAuth this round → skip `oauth2-google`

This takes about 20 minutes and shapes the first week of architecture work.

## Quality bar

A recipe ships when:

- [ ] Runs from a fresh clone with zero edits to code (only env vars)
- [ ] Has a `README.md` with the four standard sections
- [ ] No `TODO` comments in the recipe code
- [ ] `go vet` + `go test` clean
- [ ] Go version pinned in `go.mod`
- [ ] Docker-based recipes include `docker-compose.yml`

## References

- Upstream: [`gofiber/recipes`](https://github.com/gofiber/recipes)
- Complementary repos:
  - [`clean-go-starter`](https://github.com/tunacosgun/clean-go-starter)
  - [`ddd-workout-kit`](https://github.com/tunacosgun/ddd-workout-kit)

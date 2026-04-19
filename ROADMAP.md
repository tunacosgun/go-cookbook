# Roadmap

Planned additions and curation on `go-cookbook`, maintained by Tunasoft Yazılım.

## Near term

### 🚧 Webhook idempotency recipe
A dedicated `webhook-idempotent` recipe demonstrating:
- Unique constraint on provider `event_id`
- Transactional processing (event row + business state + outbox in one TX)
- Safe retry — second call returns 200 without re-running business logic
- Dead-letter handling with admin-panel surface

Today's recipes touch JWT and rate-limiting but lack a canonical webhook pattern; this is the #1 pattern we copy into commercial projects.

### 🚧 Stripe + iyzico abstraction recipe
A `payment-provider-abstraction` recipe showing a `PaymentProvider` interface with two satisfied implementations (Stripe SDK, iyzico SDK), swappable at boot. Demonstrates the abstraction-layer pattern we use so product choice of payment provider can flip without touching domain code.

### 🚧 Outbox + dispatcher recipe
Minimal end-to-end outbox pattern: a business endpoint writes both a DB row and an outbox event in one transaction; a separate goroutine dispatches events to a Redis Streams or in-process bus.

## Next

### ⏳ Recipe pruning
Upstream has grown to include many recipes we do not use in commercial delivery. We want to mark some as "upstream reference only" in our index to keep the curated set focused. Candidates: `air-live-reload`, `hot-reload`, certain DB-specific quickstarts.

### ⏳ Per-recipe `Dockerfile` convention
Not every recipe has a production Dockerfile. Adding one per recipe with multi-stage build + non-root user + tini as PID 1.

### ⏳ GitHub Actions template per recipe
A reusable workflow that runs `go test`, `go vet`, and a quick curl smoke test against the recipe's main endpoint. Enforces the "runs from a fresh clone" quality bar automatically.

## Later

### 📦 gRPC recipes
Today the cookbook is HTTP-only via Fiber. Add parallel gRPC recipes for internal-service patterns: interceptor chains, streaming, error mapping.

### 📦 Observability bundle
A bundled trio of recipes showing the full Prometheus + OpenTelemetry + slog integration in a single service. Today these are fragmented across three separate recipes; a combined "production observability" recipe would save readers 30 minutes of wiring.

### 📦 Testing recipes
A short series:
- `testing-table-driven`
- `testing-integration-with-containers`
- `testing-e2e-with-dockertest`
- `testing-http-with-httptest`

### 📦 Deploy recipes
Minimal examples for common deployment targets:
- `deploy-fly-io`
- `deploy-render`
- `deploy-k8s`
- `deploy-systemd-vps` (our default)

## Accepted, not scheduled

- `search-postgres-fulltext` recipe
- `search-meilisearch` recipe
- `caching-redis-with-ttl-jitter`
- `queue-asynq` (Redis-based task queue)

## Non-goals

- ❌ Replacing the upstream cookbook — we curate and extend, we don't fork away
- ❌ Enforcing "one recipe per problem" — some problems legitimately have multiple good solutions (e.g., gorm vs sqlc vs ent)
- ❌ Opinionated Go framework — recipes are Fiber-flavored because upstream is; we use chi in production for `clean-go-starter`

## Release cadence

Tagged when a batch of 3+ new recipes lands or a meaningful refactor across existing recipes ships.

## Contributing to the roadmap

Contact [info@tunahancosgun.dev](mailto:info@tunahancosgun.dev) to request a recipe for a commercial engagement.

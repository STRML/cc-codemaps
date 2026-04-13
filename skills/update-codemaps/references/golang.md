# Go Codemap Guidance

## Discovery Tools

- `tree -L 3 -I vendor .` for package structure
- `go list ./...` for all packages
- Read `cmd/` directories for entry points
- `go.mod` for module path, Go version, dependencies

## What to Capture

### Module Map
- Package layout: `cmd/`, `internal/`, `pkg/`, `api/`
- Entry points: `main()` in each `cmd/` binary
- Interface definitions and their implementations
- Exported vs unexported (capitalization boundary)

### Patterns
- HTTP handler organization (chi/gin/echo routers, middleware chains)
- gRPC service definitions and generated code location
- Dependency injection (wire, fx, manual constructor injection)
- Concurrency patterns (goroutines, channels, errgroup, worker pools)
- Context propagation and cancellation patterns

### Data Layer
- Struct definitions with JSON/DB tags
- Database layer (sqlc generated code, GORM models, raw sql)
- Proto definitions (`.proto` files and generated Go code)
- Config structs (viper, envconfig, koanf)

### Build & Config
- `go.mod` module path and Go version
- Build tags (`//go:build`)
- `Makefile` or `mage` targets
- Test organization (`_test.go` files, testdata/, test helpers)

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Package layout, dependency graph, entry points |
| `backend.md` | Handlers, services, middleware, workers |
| `data.md` | Core types, proto definitions, DB models |
| `integrations.md` | External APIs, gRPC clients, message queues |

# Rust Codemap Guidance

## Discovery Tools

- `tree -L 3 -I target src/` for module structure
- `cargo modules structure` for module graph (if installed)
- Read `lib.rs` / `main.rs` for module declarations and re-exports
- `Cargo.toml` for workspace members, features, dependencies

## What to Capture

### Module Map
- Crate structure: binary vs library, workspace members
- `mod` tree from `lib.rs`/`main.rs` (pub vs private modules)
- Re-exports and public API surface (`pub use`)
- Feature flags and conditional compilation (`#[cfg(feature = "...")]`)

### Patterns
- Trait definitions and their implementors
- Error types and error handling strategy (thiserror/anyhow)
- Builder patterns, newtype wrappers
- Async runtime choice (tokio/async-std) and task spawning patterns
- State management (Arc<Mutex<T>>, channels, actor model)

### Data Layer
- Core structs with derive macros (Serialize, Clone, etc.)
- Enum variants (especially protocol/state machine enums)
- Database integration (sqlx queries, diesel schema, sea-orm entities)
- Config structs (clap args, serde config files)

### Build & Config
- Workspace layout and inter-crate dependencies
- Feature flag matrix
- Build scripts (`build.rs`)
- Test organization (`#[cfg(test)]` modules vs `tests/` integration)

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Crate/workspace layout, module graph, features |
| `backend.md` | Per-module breakdown, trait hierarchy |
| `data.md` | Core types, enums, error types, config |

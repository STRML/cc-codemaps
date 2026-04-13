# cc-codemaps

A Claude Code plugin that generates token-lean architecture maps for any codebase. Maps load into context at session start, giving Claude accurate structural knowledge without burning tokens on full file reads.

## Install

```bash
claude plugin add STRML/cc-codemaps
```

## Usage

```
/update-codemaps
```

The skill auto-detects your project's language from `CLAUDE.md`, `README.md`, or build system markers (`package.json`, `Cargo.toml`, `go.mod`, `platformio.ini`, `pyproject.toml`), then loads language-specific guidance and generates maps into `codemaps/`.

## What it generates

| File | When |
|------|------|
| `architecture.md` | Always. System overview, module graph, build envs, data flow |
| `backend.md` / `firmware.md` | Per-module breakdown with key functions/classes |
| `frontend.md` | Only for projects with a frontend |
| `data.md` | Core types, schemas, constants, config objects |
| `integrations.md` | External APIs, third-party SDKs |
| `workers.md` | Background jobs, queues, cron tasks |

Files that don't apply are skipped. Stale files are pruned.

## Supported languages

- TypeScript / JavaScript
- C / C++ (including embedded/firmware)
- Python
- Rust
- Go

Each language has a reference file with discovery tools, what-to-capture guidance, and codemap file suggestions. Adding a new language is one markdown file in `skills/update-codemaps/references/`.

## Design principles

- **Token-lean**: tables, code blocks, ASCII diagrams. No filler prose. Target under 200 lines per file.
- **Accuracy over coverage**: only documents what was verified by reading code.
- **Fully generated**: codemaps are overwritten on each run. Project-specific notes belong in `CLAUDE.md`.
- **Safe**: never modifies `CLAUDE.md` or `README.md` without explicit user approval.

## License

MIT

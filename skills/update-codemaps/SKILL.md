---
name: update-codemaps
description: "Regenerate token-lean architecture maps in codemaps/. Auto-detects project language, scans codebase structure, writes maps that load into context at session start."
user_invocable: true
---

# Update Codemaps

Regenerate the token-lean architecture maps in `codemaps/` from the current state of the codebase. These maps are loaded at session start and directly affect correctness of future edits.

## Step 1: Detect Project Language & Structure

Read `CLAUDE.md` and `README.md` to identify:
- Primary language(s) and framework(s)
- Build system and entry points
- Source directory layout
- Test framework

**Fallback**: If docs are missing or don't mention the language, scan for build system markers:

| Marker file | Language |
|------------|----------|
| `package.json`, `tsconfig.json` | TypeScript/JavaScript |
| `Cargo.toml` | Rust |
| `go.mod` | Go |
| `platformio.ini`, `CMakeLists.txt`, `Makefile` | C/C++ |
| `pyproject.toml`, `setup.py`, `requirements.txt` | Python |

Then load the matching language reference(s) from `references/` for language-specific guidance on what to capture and which tools to use. Available references: `typescript.md`, `cpp.md`, `python.md`, `rust.md`, `golang.md`. Load only the ones that apply.

For multi-language projects (e.g., a C++ firmware repo with a Rust TUI tool), load all relevant references. Create one `architecture.md` for the overall system, with separate per-subsystem files named by component (e.g., `firmware.md`, `viz.md`) rather than generic names.

## Step 2: Decide Which Codemap Files to Generate

Based on the project structure, choose which files to create in `codemaps/`. Common patterns:

| File | When |
|------|------|
| `architecture.md` | Always. System overview, module graph, build envs, data flow |
| `backend.md` or `firmware.md` | Per-module breakdown with key functions/classes |
| `frontend.md` | Only for projects with a frontend (React, Vue, etc.) |
| `data.md` | Core types, schemas, constants, config objects |
| `integrations.md` | External APIs, third-party SDKs |
| `workers.md` | Background jobs, queues, cron tasks |

Don't create files that don't apply. A C++ firmware project has no `frontend.md`. A static site has no `workers.md`.

**Pruning**: If `codemaps/` already exists, check for files that no longer match the project structure (e.g., a `frontend.md` for a project that dropped its frontend). Delete stale files to prevent future sessions from loading outdated context.

## Step 3: Scan the Codebase

Use the techniques from the loaded language reference(s):
- Read directory structure (`tree`)
- Read headers/interfaces/types for public API surface
- Read build config for environments and flags
- Read existing codemaps to understand current format

Don't read every file line-by-line. Use symbol overviews, function signatures, and structural analysis. Limit scanning to ~20 key files per codemap — if the project has more modules, focus on top-level ones and note uncovered areas.

**Tool fallbacks**: Language references suggest specialized tools (ts-morph, madge, cargo modules). If these aren't installed, fall back to standard tools (tree, grep, file reads). Never attempt to install tools or run commands with side effects (e.g., `npx madge --image` writes to the repo — skip it).

## Step 4: Write the Codemaps

Every codemap file starts with:
```
> Generated: YYYY-MM-DD | Token-lean format for LLM context
```

Rules:
- **Token-lean**: tables, code blocks, ASCII diagrams. No filler prose
- **Accuracy over coverage**: only document what you verified by reading code
- **Preserve existing format**: if codemaps already exist, match their section structure unless it needs to change
- **Constants and types**: pull actual values from source, not from memory
- **Codemaps are fully generated**: user edits will be overwritten on the next run. Add project-specific notes to CLAUDE.md, not codemaps
- **Size target**: aim for under 200 lines per codemap file

## Step 5: Diff and Report

After writing, diff each file against the previous version. Report what changed: new sections, removed sections, updated values.

If any file is being created for the first time or deleted, note it. For updates, show the diff summary. Always proceed — the user can review the git diff and revert if needed.

## Step 6: Suggest Documentation Updates

After updating codemaps, **suggest** (do not automatically apply) documentation changes:

1. If `CLAUDE.md` duplicates architecture details that now live in codemaps, list the sections that could be replaced with references (e.g., "The Module Dependency Graph in CLAUDE.md duplicates codemaps/architecture.md — consider replacing with a link").
2. If `README.md` doesn't mention codemaps, suggest adding a line.
3. Principle: architecture details live in codemaps, constraints and rules live in CLAUDE.md, setup instructions live in README.md.

**Do NOT modify CLAUDE.md or README.md without explicit user approval.** These files are hand-curated and authoritative. Codemaps are generated derivatives. Only list suggestions and let the user decide.

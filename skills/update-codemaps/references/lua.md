# Lua Codemap Guidance

## Discovery Tools

- `tree -L 3 .` for module structure
- Read entry files: `init.lua` (Hammerspoon/Neovim), `main.lua` (LOVE2D), `conf.lua`
- Search for module definitions (patterns like `^local M = `, `^function `, `return {` at end of files)
- Check for framework markers: `hs.` (Hammerspoon), `vim.` (Neovim), `love.` (LOVE2D)

## What to Capture

### Module Map
- Entry point: `init.lua`, `main.lua`, or configured entry
- Module loading pattern (`require` calls and return tables)
- Global vs local scope boundaries
- Plugin/Spoon structure (Hammerspoon), plugin spec (Neovim lazy.nvim)

### Framework Patterns
- **Hammerspoon**: Spoon loading, hotkey bindings, watchers, menubar items
- **Neovim**: Plugin manager config, keymaps, autocommands, LSP setup
- **LOVE2D**: Callback functions (`love.load`, `love.update`, `love.draw`), state management
- **OpenResty/nginx**: Request phases, shared dictionaries, cosocket usage

### Data Layer
- Configuration tables and their structure
- State management (module-local tables, global state)
- File I/O patterns, JSON/config parsing
- SQLite or LuaSQL usage (if applicable)

### Build & Config
- LuaRocks dependencies (`*.rockspec`)
- Embedded Lua version (5.1/5.4/LuaJIT)
- Test framework: busted, luaunit
- Build integration: Makefile, CMake (for C modules)

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Module graph, entry points, framework integration |
| `data.md` | Config tables, state management, persistence |

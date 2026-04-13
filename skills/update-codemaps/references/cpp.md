# C/C++ Codemap Guidance

## Discovery Tools

- `tree -L 2 -d src/ include/ test/` for directory structure
- Search for function signatures (e.g., patterns like `^void `, `^bool `, `^static ` in `src/`)
- Read header files for public API surface (`.h` files define the contract)
- Check build system: `CMakeLists.txt`, `platformio.ini`, `Makefile`, `meson.build`

## What to Capture

### Module Map
- Entry points: `main()`, `setup()`/`loop()` (Arduino), `app_main()` (ESP-IDF)
- Header dependency graph (which `.h` includes which)
- Compilation units and what they export
- Conditional compilation (`#ifdef` blocks that gate major features)

### Embedded/Firmware Patterns
- Pin assignments and hardware abstraction
- Interrupt service routines (ISRs) and shared volatile state
- State machines (enum + struct + update function)
- Timer/peripheral configuration
- Build environments and target boards

### Data Layer
- Core structs and typedefs (from headers)
- Enum definitions with values (especially protocol enums)
- Global/extern variables and their ownership
- Compile-time constants and configuration macros
- Communication protocols (CAN IDs, UART framing, SPI registers)

### Build & Config
- Build environments and their flags
- Platform-specific `#ifdef` branches
- Library dependencies
- Test framework and test discovery pattern

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | System overview, module graph, build envs, data flow |
| `backend.md` or `firmware.md` | Per-module breakdown with key functions |
| `data.md` | Structs, enums, constants tables, pin maps |
| `hardware.md` | Pin assignments, peripherals, electrical notes (if complex) |

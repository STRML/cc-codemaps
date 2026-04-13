# C# / .NET Codemap Guidance

## Discovery Tools

- `tree -L 3 -I bin -I obj .` for solution structure
- Read `*.sln` for project list, `*.csproj` for dependencies and target framework
- Search for class definitions (patterns like `^class `, `^interface `, `^record ` in source dirs)
- Check for framework markers: `Program.cs` with `WebApplication.CreateBuilder` (ASP.NET), `MainWindow.xaml` (WPF/MAUI)

## What to Capture

### Module Map
- Solution/project structure (`.sln` → `.csproj` references)
- Entry points: `Program.cs`, `Startup.cs`, top-level statements
- Namespace organization and project references
- Interface definitions and DI registrations

### Framework Patterns
- **ASP.NET Core**: Minimal API or controller-based routes, middleware pipeline, `Program.cs` service registration
- **Blazor**: Component hierarchy, render modes (Server/WASM/Auto)
- **WPF/MAUI**: MVVM pattern, view/viewmodel bindings
- **Worker Services**: `BackgroundService` implementations, hosted services
- Dependency injection: `builder.Services` registrations, interface→implementation mappings

### Data Layer
- Entity Framework Core: DbContext, entity classes, migrations (`Migrations/`)
- Dapper queries, stored procedures
- DTOs and AutoMapper/Mapster profiles
- Configuration: `appsettings.json` sections, `IOptions<T>` bindings

### Build & Config
- `.csproj` target framework, NuGet dependencies, project references
- `appsettings.json` / `appsettings.{Environment}.json` structure
- Test framework: xUnit, NUnit, MSTest, test project organization
- Docker support: `Dockerfile`, multi-stage builds

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Solution layout, project references, DI registrations |
| `backend.md` | Controllers/endpoints, services, middleware, workers |
| `frontend.md` | Blazor components, MAUI views (if applicable) |
| `data.md` | Entities, DbContext, migrations, DTOs |

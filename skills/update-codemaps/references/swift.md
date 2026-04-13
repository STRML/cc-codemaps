# Swift Codemap Guidance

## Discovery Tools

- `tree -L 3 -I .build -I DerivedData Sources/` or project directory for structure
- Read `Package.swift` (SPM) or check `.xcodeproj`/`.xcworkspace` for targets
- Search for type definitions (patterns like `^class `, `^struct `, `^protocol `, `^enum ` in `Sources/`)
- Check for framework markers: `@main` (app entry), `ContentView` (SwiftUI), `AppDelegate` (UIKit)

## What to Capture

### Module Map
- Package/target structure from `Package.swift` or Xcode project
- Entry points: `@main`, `AppDelegate`, `SceneDelegate`
- Module boundaries and access control (`public`, `internal`, `private`)
- Protocol definitions and conformances

### Framework Patterns
- **SwiftUI**: View hierarchy, `@State`/`@Binding`/`@Observable` data flow, navigation
- **UIKit**: ViewController hierarchy, storyboard vs programmatic, coordinator pattern
- **SPM**: Package targets, dependencies, plugins
- **Vapor** (server-side): Route collections, middleware, Fluent models

### Data Layer
- Model structs/classes with `Codable` conformance
- Core Data models or SwiftData `@Model` classes
- Networking layer (URLSession, Alamofire, async/await patterns)
- UserDefaults, Keychain, and persistence patterns

### Build & Config
- `Package.swift` targets and dependencies
- Xcode build configurations and schemes
- Test targets: XCTest, Swift Testing framework
- Platform targets (iOS, macOS, watchOS, visionOS)

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Target layout, module graph, platform targets |
| `frontend.md` | View hierarchy, navigation, state management (SwiftUI/UIKit apps) |
| `data.md` | Models, persistence, networking layer |
| `backend.md` | Server-side routes, middleware, database (Vapor) |

# Ruby Codemap Guidance

## Discovery Tools

- `tree -L 3 -I vendor -I tmp -I log .` for project structure
- Read `Gemfile` for dependencies and gem groups
- Search for class/module definitions (patterns like `^class `, `^module ` in `app/` or `lib/`)
- Check for framework markers: `config/routes.rb` (Rails), `config.ru` (Rack)

## What to Capture

### Module Map
- Entry points: `config.ru`, `bin/rails`, `Rakefile`, CLI binstubs
- App directory structure (`app/models`, `app/controllers`, `app/services`)
- Lib modules and their autoload paths
- Gem/engine structure for multi-gem repos

### Framework Patterns
- **Rails**: MVC layers, route definitions, concerns, ActiveJob queues, ActionCable channels
- **Sinatra/Rack**: Route definitions, middleware stack
- **CLI**: Thor/GLI command groups, option parsing
- Mixin patterns: concerns, modules included in models/controllers

### Data Layer
- ActiveRecord models, associations, scopes, validations
- Database migrations (`db/migrate/`)
- Serializers (ActiveModel::Serializer, Blueprinter, jbuilder)
- Config objects (Rails credentials, environment variables)

### Build & Config
- `Gemfile` groups (development, test, production)
- `config/` directory structure (initializers, environments)
- Test framework: RSpec (`spec/`), Minitest (`test/`), factory setup
- Background jobs: Sidekiq, DelayedJob, GoodJob

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | App structure, gem dependencies, route overview |
| `backend.md` | Controllers, services, jobs, mailers |
| `data.md` | Models, associations, migrations, serializers |
| `integrations.md` | External APIs, webhooks, third-party gems |

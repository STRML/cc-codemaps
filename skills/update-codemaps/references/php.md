# PHP Codemap Guidance

## Discovery Tools

- `tree -L 3 -I vendor -I node_modules .` for directory structure
- Read `composer.json` for dependencies, autoload mappings, and scripts
- Search for class definitions (patterns like `^class `, `^abstract class `, `^interface ` in source directories)
- Check for framework markers: `wp-content/` (WordPress), `artisan` (Laravel), `bin/console` (Symfony)

## What to Capture

### Module Map
- Entry points: `index.php`, `functions.php` (WordPress), `routes/` (Laravel), plugin main files
- Autoload structure from `composer.json` (PSR-4 namespaces → directories)
- Hook/filter registration points (WordPress `add_action`, `add_filter`)
- Plugin/theme hierarchy and activation flow

### Framework Patterns
- **WordPress**: Theme structure (`functions.php`, template hierarchy), plugin entry files, custom post types, REST API endpoints, WooCommerce hooks
- **WooCommerce**: Payment gateways, shipping methods, product types, checkout fields, order processing hooks
- **Laravel**: Route files, controllers, middleware, service providers, Eloquent models, migrations
- **Symfony**: Bundle structure, service definitions, event subscribers

### Data Layer
- Database access: `$wpdb` queries, Eloquent models, Doctrine entities, raw PDO
- Custom tables and schema definitions (WordPress `dbDelta`, Laravel migrations)
- Options/settings API usage (WordPress `get_option`, Laravel config)
- REST API endpoint definitions and response schemas

### Build & Config
- `composer.json` autoload and dependency structure
- WordPress plugin headers (Plugin Name, Version, etc.)
- Environment config (`.env`, `wp-config.php`, `config/`)
- Build tools: webpack/vite for frontend assets alongside PHP

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Plugin/theme structure, hook registration flow, dependencies |
| `backend.md` | Controllers/handlers, REST endpoints, admin pages |
| `data.md` | Database schema, custom tables, options, post types |
| `integrations.md` | External APIs, payment gateways, shipping providers |

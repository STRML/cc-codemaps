# Python Codemap Guidance

## Discovery Tools

- `tree -L 3 -I __pycache__ -I .venv -I venv src/` for structure
- Search for class and function definitions (patterns like `^class `, `^def `, `^async def ` in `src/`)
- Read `__init__.py` files to understand package exports
- Check `pyproject.toml`, `setup.py`, or `setup.cfg` for entry points

## What to Capture

### Module Map
- Package structure and `__init__.py` re-exports
- Entry points: CLI (`console_scripts`), ASGI/WSGI app factory, `__main__.py`
- Route definitions (FastAPI routers, Django urlpatterns, Flask blueprints)
- Middleware and dependency injection (FastAPI `Depends`, Django middleware)

### Framework Patterns
- **FastAPI/Django/Flask**: Route organization, middleware stack, background tasks
- **CLI**: Click/Typer command groups, argument parsing
- **Data pipeline**: DAG definitions (Airflow), task chains (Celery)
- **ML**: Model loading, inference pipeline, training loop structure

### Data Layer
- ORM models (SQLAlchemy, Django models, Tortoise)
- Pydantic schemas / dataclasses / TypedDict definitions
- Database migrations (Alembic, Django migrations)
- Config management (pydantic-settings, dynaconf, environ)

### Build & Config
- Dependency management: `pyproject.toml` vs `requirements.txt`
- Virtual environment expectations
- Test framework: pytest fixtures, conftest.py hierarchy
- Type checking: mypy/pyright config, `py.typed` markers

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Package layout, dependency graph, entry points |
| `backend.md` | Routes, services, middleware, background tasks |
| `data.md` | Models, schemas, migrations, config objects |
| `integrations.md` | External APIs, SDK wrappers, message queues |

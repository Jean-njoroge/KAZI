# Contributing to KAZI

Thank you for considering a contribution to KAZI. This document explains how the project is organized, what kinds of contributions are welcome, and how to submit your work.

---

## How KAZI is Structured

KAZI is a platform with a plugin architecture. The core platform lives in `src/kazi/` and provides orchestration, scoring, template rendering, and delivery. Domain plugins live in separate directories under `domains/` and define their own agents, scoring rubrics, and templates.

| Directory | Owns |
|-----------|------|
| `src/kazi/` | Platform core (orchestrator, base classes, scoring engine, renderer) |
| `api/` | FastAPI server, plugin loader, routes |
| `cli/` | Command-line interface (`kazi init`, `kazi run`, `kazi serve`) |
| `domains/_template/` | Starter template for new domains |
| `examples/` | Working code examples for documentation |
| `docs/` | Guides and reference documentation |

---

## What We Welcome

**Domain plugins.** The highest-value contribution is a new domain that demonstrates KAZI's flexibility. If you have expertise in a professional services vertical (consulting, research, compliance, content production), consider building a domain plugin.

**Platform improvements.** Bug fixes, performance improvements, and new platform-level features (new base agent types, scoring enhancements, template helpers) are welcome.

**Documentation.** Clearer explanations, better examples, typo fixes, and translations all help.

**Tests.** Additional test coverage for platform core or example domains.

---

## Creating a New Domain Plugin

The fastest path to a meaningful contribution:

```bash
kazi init my-domain
```

This creates `domains/my-domain/` with the required structure. From there:

1. Define your `manifest.yaml` with pipeline stages and scoring config
2. Write agents in `agents/` extending `BaseAgent` or its subclasses
3. Create a `scoring.yaml` with dimensions appropriate to your vertical
4. Build HTML templates in `templates/`
5. Add a `routes.py` with at least a `/health` endpoint
6. Write tests in `tests/`

See `docs/plugins.md` for the full domain plugin specification.

---

## Submitting a Pull Request

1. **Fork** the repository and create a branch from `main`
2. **Make your changes** following the conventions below
3. **Test** your changes locally (`pytest` for Python, verify templates render)
4. **Commit** with a clear message following the format below
5. **Open a PR** against `main` with a description of what changed and why

### Commit Message Format

```
type: short description

Longer explanation if needed.
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

Examples:
- `feat: add confidence decay to base scorer`
- `docs: clarify pipeline trigger types`
- `fix: handle empty tool response in BaseAgent`

---

## Code Conventions

**Python style.** Follow PEP 8. Use type hints on all public methods. Prefer `async def` for agent `run()` methods.

**Agent naming.** Agent class names use PascalCase (`MarketScout`). The `name` attribute uses snake_case (`market_scout`).

**Scoring dimensions.** Use lowercase snake_case for dimension names in `scoring.yaml`. Keep weights as integers that sum to 100.

**Templates.** Self-contained HTML with inline CSS. No external dependencies. Include print/PDF page breaks between major sections.

**Tests.** Place tests in a `tests/` directory within the domain or at the project root. Use `pytest`. Mock external API calls.

---

## What We Do Not Accept

- Code that exposes client data, real engagement IDs, or proprietary scoring rubrics
- Dependencies on paid APIs without a clear mock/stub path for testing
- Changes that break domain isolation (one domain importing from another directly)
- Untested agents or scoring configurations

---

## Questions

Open an issue with the `question` label, or start a discussion in the Discussions tab. We respond within a few days.

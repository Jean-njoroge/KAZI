# Changelog

All notable changes to KAZI are documented in this file. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.0] - 2026-05-08

Initial open-source release of the KAZI platform.

### Added

- **Platform core** (`src/kazi/`): BaseAgent, Pipeline, FanOut, Orchestrator, ScoreLegend, ReviewQueue, TemplateRenderer
- **Plugin system**: manifest.yaml-driven domain discovery and registration
- **Scoring engine**: multi-dimensional scoring with configurable tiers, confidence decay, and drift detection
- **Template renderer**: Jinja2 to HTML to PDF pipeline with HITL markers and print-ready formatting
- **CLI**: `kazi init`, `kazi run`, `kazi serve` commands
- **API server**: FastAPI with automatic domain route mounting
- **Domain template** (`domains/_template/`): starter scaffold for new domain plugins
- **Examples**: hello_agent, scout_score_pipeline, weekly_brief
- **Documentation**: 7 guides covering architecture, design patterns, building agents, scoring, templates, and plugins

### Architecture Decisions

- Domain-agnostic platform: any professional services vertical can plug in via manifest.yaml
- Agents are stateless and async; state lives in the shared context dict passed through the pipeline
- Scoring is declarative (YAML-defined) rather than hardcoded
- Templates are self-contained HTML with no external dependencies
- Domain isolation enforced at database (separate schemas), API (separate prefixes), and agent (namespaced registry) levels

---

## [Unreleased]

_Tracking upcoming work here._

- Community domain examples (contributions welcome)
- GitHub Actions CI workflow
- PyPI package publication
- Dashboard frontend (React shell with plugin page loading)

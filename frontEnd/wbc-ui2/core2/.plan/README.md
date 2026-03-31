# WBC-UI2 Internal Planning Hub

> **PRIVATE** — This folder is the internal planning, strategy, and technical reference for the wbc-ui2 ecosystem. Nothing here should be published directly. Public-facing content lives in `.github/`.

---

## Document Index

| Document | Purpose | Scope |
|----------|---------|-------|
| [vision.md](vision.md) | Why wbc-ui2 exists, market positioning, core thesis | Strategic |
| [roadmap.md](roadmap.md) | Phased execution plan (2026-2027) | Strategic |
| [architecture.md](architecture.md) | Monorepo engineering, build system, module structure | Technical |
| [monetization.md](monetization.md) | Free vs Pro tiering, pricing, feature gating | Business |
| [audit.md](audit.md) | Code quality assessment, gap analysis, recommendations | Review |
| [changelog.md](changelog.md) | Significant architectural decisions and changes | Historical |
| [cli-guide.md](cli-guide.md) | CLI scaffolding architecture and usage | Technical |

## Subdirectories

| Folder | Purpose |
|--------|---------|
| [.github/](.github/) | Public-ready articles for `wb-labs/.github` repo |
| [templates/](templates/) | Pattern templates for scaffolding new packages |
| [tasks/](tasks/) | Prioritized work items (P0/P1/P2) |
| [issues/](issues/) | Known bugs and problems (P0/P1/P2) |

## Per-Package Planning

Each sub-package in `src/wb-*/` mirrors this structure with its own `.plan/` folder containing package-specific roadmap, monetization, licensing, changelog, tasks, and issues.

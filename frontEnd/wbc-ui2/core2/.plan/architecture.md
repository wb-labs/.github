# WBC-UI2 — Monorepo Architecture & Engineering Guide

> **PRIVATE** — Internal maintainer reference. Do NOT expose in public documentation.

---

## 1. Architecture Overview

The monorepo uses **NPM Workspaces** to manage the entire ecosystem. It separates the "Core Engine" from "Premium Modules" while sharing a centralized build and packaging infrastructure.

```
core2/
├── .plan/              # Internal planning hub
├── assets/logos/       # Brand assets
├── src/                # Monorepo source
│   ├── wb-core/        # wbc-ui2 — The Core Engine
│   ├── wb-code/        # @wbc-ui2/code
│   ├── wb-chart/       # @wbc-ui2/chart
│   ├── wb-latex/       # @wbc-ui2/latex
│   ├── wb-mermaid/     # @wbc-ui2/mermaid
│   ├── wb-table/       # @wbc-ui2/table (coming soon)
│   ├── wb-gis/         # @wbc-ui2/gis (coming soon)
│   ├── wb-dataviewer/  # @wbc-ui2/wbDataviewer (coming soon)
│   ├── wb-alert/       # @wbc-ui2/alert
│   ├── wb-office/      # @wbc-ui2/office
│   ├── wb-timetable/   # Scheduling component
│   ├── wbc-wiki-obj/   # Sample data and wiki objects
│   ├── wb-vuepressThemeWb2/ # VuePress theme for docs
│   ├── wb-cli/         # @wbc-ui2/cli
│   ├── pkg_cli/        # Build/packaging CLI tools
│   ├── apps/           # All demos, docs portals, starter templates
│   └── wbc-tgz-bundles/ # Centralized build artifacts
├── README.md           # Public-facing
├── DEVELOPER.md        # Internal commands reference
├── package.json        # Root monorepo manifest
└── .gitignore
```

---

## 2. The Freemium Build Matrix (`WBC_PRO`)

| Mode | Environment | Target | Description |
|:---|:---|:---|:---|
| **Default** | `WBC_PRO=undefined` | Local Development | All features enabled (God Mode) |
| **Free** | `WBC_PRO=false` | Public NPM | Premium code stripped |
| **Pro** | `WBC_PRO=true` | Private Sales | All premium functionality |

### Compile-Time Flags

| Flag | Source | True When |
|:---|:---|:---|
| `__WBC_DEV__` | `vite-plugin.js` | `WBC_PRO` env var is **not set** (owner mode) |
| `__WBC_PRO__` | `vite-plugin.js` | `WBC_PRO=true` |

### Three Development Scenarios

| Script | `__WBC_DEV__` | `__WBC_PRO__` | `userTier` | Purpose |
|:---|:---|:---|:---|:---|
| `serve_vite` | `true` | `false` | `"development"` | Owner mode |
| `serve_vite:free` | `false` | `false` | `"free"` | Simulate free user |
| `serve_vite:pro` | `false` | `true` | `"premium"` | Simulate premium user |

---

## 3. Monorepo Scripts Reference

### Library Commands (`wb-*`)

| Command | Description |
|:---|:---|
| `npm run build:libs:dev` | Standard build of all libraries |
| `npm run pack:libs:dev` | Package all libs into `wbc-tgz-bundles/dev/` |
| `npm run clean:all` | Sanitize every tier folder in all workspaces |

### Application Commands (`apps/*`)

| Command | Description |
|:---|:---|
| `npm run build:apps:dev` | Mass-build all application templates |
| `npm run pack:apps:dev` | Package all apps into `wbc-tgz-bundles/apps/dev/` |
| `npm run serve:vite` | Serve primary application in dev mode |

### Individual Package Build

```bash
npm run build -w wbc-ui2
npm run build -w @wbc-ui2/code
npm run build -w @wbc-ui2/chart
```

---

## 4. Build Signatures & Isolation

Every build generates a `build-info.json` metadata file inside the output directory.

Each tier is isolated in its own directory:
- `dist-dev/` — Default developer builds
- `dist-free/` — Free-tier users
- `dist-pro/` — Premium users

### Centralized Bundle Repository

```
src/wbc-tgz-bundles/
├── dev/       # Lib bundles (source: dist-dev/)
├── free/      # Lib bundles (source: dist-free/)
├── pro/       # Lib bundles (source: dist-pro/)
└── apps/      # Application Template Repository
    ├── dev/
    ├── free/
    └── pro/
```

---

## 5. Dependency Management

### Installation Rules
- **NEVER** run `npm install` inside an app directory
- **ALWAYS** run from the monorepo root: `npm install`
- This hoists all dependencies, preventing "Duplicate Vue" errors

### Adding Dependencies

```bash
npm install axios -w @wbc-ui2-apps/md.wbc-ui.com
```

### Vite/Webpack Aliases (Critical)

All app configs must resolve to the **same** Vue instance:

```javascript
// vite.config.js
resolve: {
  alias: {
    'vue': path.dirname(require.resolve('vue/package.json')) + '/dist/vue.esm.js',
    '@wbc-ui2/code': path.resolve(__dirname, '../../../wb-code/src/index.js'),
  }
}
```

---

## 6. Unified Tier System (Dev/Free/Pro)

### Tier-Detection Logic

| Property | Description | Mode |
|:---|:---|:---|
| `__DEV__` | Injected via Vite/Webpack. True ONLY in owner mode. | Developer |
| `isWb[Pkg]Pro` | Valid license in central store. | Premium |
| `userTier` | Returns `'development'`, `'premium'`, or `'free'`. | Universal |

### Licensing Flow (Per Package)

1. **Persistence Recovery**: Load from cookie (`_wbc_[pkg]_auth`)
2. **Simulation Check**: Detect `WBC_SIMULATE_PRO` key
3. **Network Validation**: Async ping to licensing API (if needed)
4. **State Hydration**: Commit to unified `tiers` object in store

### Cookie Conventions

| Parameter | Pattern |
|:---|:---|
| Cookie Name | `_wbc_[pkg]_auth` |
| Store Slug | `[pkg_slug]` |
| Persistence | 86400 seconds (24 hours) |

---

## 7. Adding New Packages

### CLI Method

```bash
npm run create:lib <name>
```

### Manual Checklist

1. Add centralized `tiers` entry in `wb-core/src/store/index.js`
2. Implement `created()` hook with cookie-checking & simulation support
3. Gate premium UI features behind the `isAuthorized` flag
4. Define minification rules to strip PRO blocks in free builds
5. Create `.plan/` folder with package-specific docs

---

## 8. Validation & Release Flow

```
wb-<pkg>/src/ (SOURCE OF TRUTH)
    |
    v
apps/wb-<pkg>/<pkg>_demo/ (validate: does it work?)
    |
    v
apps/wb-<pkg>/<pkg>_docs/ (document: what does it do?)
    |
    v
apps/wb-<pkg>/<pkg>_template_*/ (scaffold: starter project)
    |
    v
.plan/.github/ (promote: public articles)
```

### Release Checklist

1. Clean `/dist` from previous builds
2. Run all verification tests
3. Update local changelog
4. NPM publish with appropriate access tokens
5. Verify: `npm install` works in clean environment
6. Verify: All template links are reachable
7. Verify: Documentation site is live

---

## 9. CLI Tools (`/src/pkg_cli`)

| Tool | Purpose |
|:---|:---|
| `build_libs.js` / `build_apps.js` | Symmetrical build orchestrators |
| `pack_libs.js` / `pack_apps.js` | Symmetrical packaging orchestrators |
| `unify_scripts.js` | Cross-workspace mass script sync |
| `clean_libs.js` | Global sanitization for monorepo |
| `create_lib.js` | Automated package generation |

---

*Consolidated from: `technical/MONOREPO_ENGINEERING_GUIDE.md`, `technical/pkg_architecture_monetization_2026.md`, `package_blueprint.md`, `technical/pkg_licensing_flow.md`*

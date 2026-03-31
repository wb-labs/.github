# WBC-UI2 — Changelog (Strategic & Architectural Decisions)

> Tracks significant architectural decisions and code changes that impact monetization, user-tier, and security strategy.

---

## 2026-03-31 — Documentation Restructure

### Project Structure Overhaul
- Merged `strategy/` + `technical/` + `claude/` into unified `.plan/` folder
- Created prioritized `tasks/` and `issues/` directories
- Added `.github/` folders for public-ready content
- Cleaned up duplicate assets, archive folders, and stray files
- Established per-package `.plan/` pattern mirroring root structure

---

## 2026-03-20 — User Tier Architecture & Global Exposure Refactoring

### 1. New Compile-Time Variable: `__WBC_DEV__`

**Files changed**: `vite-plugin.js`, `WBC.js`

Introduced `__WBC_DEV__` as the primary control for developer/owner mode:

```javascript
'__WBC_DEV__': JSON.stringify(process.env.WBC_PRO === undefined)
```

- `true` only when `WBC_PRO` env var is **not set** (owner/developer mode)
- `false` when `WBC_PRO` is explicitly set to `true` OR `false` (simulation mode)

### 2. Three Development Scenarios

| Script | `__WBC_DEV__` | `__WBC_PRO__` | `userTier` | Purpose |
|:---|:---|:---|:---|:---|
| `serve_vite` | `true` | `false` | `"development"` | Owner mode |
| `serve_vite:free` | `false` | `false` | `"free"` | Simulate free user |
| `serve_vite:pro` | `false` | `true` | `"premium"` | Simulate premium user |

**Breaking change**: `serve_vite` no longer sets `WBC_PRO=true`.

### 3. `userTier` and `license` on `itemAccessebility`

New properties added to `itemAccessebility` (centralized in Vuex):
- `userTier`: `"development"` | `"free"` | `"premium"` — always present
- `license`: `{ premiumKey, expiresAt, customer, status }` — present when `isPro`

### 4. `toggleWbCode` / `toggleWbCodeFile` — Extended to PRO

Guard changed from `if (__DEV__)` to `if (__DEV__ || isPro)`.

### 5. Global Exposure — Two-Level Architecture

**Level 1 (ALL users)**: Explicit `global` prop only — user chooses the name.
**Level 2 (DEV only)**: Blanket exposure of all named instances + raw `_vm`.

### 6. Vuex Store: `_wbcProDetails`

Added state, mutation, and getter for detailed license information.

### 7. Performance: Centralized Tier Detection

Removed expensive per-component re-evaluation. Tier resolution now O(1) via store getters. Significant boost for pages with 4000+ components.

### 8. Feature Reclassification: `root` is now Premium

`itemAccessebility.root` moved from Free to Pro. Provides direct access to `$store`, `$router`, and full app tree — an "Architect" feature.

---

*Consolidated from: `technical/pkg_changelog.md`, `wb-core/technical/wb-core_changelog_2026.md`*

# wb-core: Changelog

> Source: `technical/wb-core_changelog_2026.md`

---

## 2026-03-20 -- User Tier Architecture & Global Exposure Refactoring

### 1. New Compile-Time Variable: `__WBC_DEV__`

**Files changed**: `vite-plugin.js`, `WBC.js`

Introduced `__WBC_DEV__` as the primary control for developer/owner mode:

```javascript
// vite-plugin.js
'__WBC_DEV__': JSON.stringify(process.env.WBC_PRO === undefined)
```

- `true` only when `WBC_PRO` env var is **not set** (owner/developer mode)
- `false` when `WBC_PRO` is explicitly set (simulation mode)

`__DEV__` in `WBC.js` now checks `__WBC_DEV__` first, falling back to `NODE_ENV` for non-Vite builds:

```javascript
const __DEV__ = typeof __WBC_DEV__ !== 'undefined'
    ? __WBC_DEV__
    : (typeof process !== 'undefined' && process.env
        ? process.env.NODE_ENV !== 'production'
        : false);
```

**Rationale**: Vite hardcodes `NODE_ENV` to `'development'` in dev server mode, making the old `__DEV__` always `true`.

### 2. Three Development Scenarios

**Files changed**: `package.json`, `vite-plugin.js`

| Script | `WBC_PRO` env | `__WBC_DEV__` | `__WBC_PRO__` | `userTier` | Purpose |
|---|---|---|---|---|---|
| `serve_vite` | *not set* | `true` | `false` | `"development"` | Owner mode -- everything accessible |
| `serve_vite:free` | `"false"` | `false` | `false` | `"free"` | Simulates free production user |
| `serve_vite:pro` | `"true"` | `false` | `true` | `"premium"` | Simulates premium production user |

**Breaking change**: `serve_vite` no longer sets `WBC_PRO=true`.

### 3. `userTier` and `license` on `itemAccessebility`

**Files changed**: `WBC.js`, `store/index.js`

- **`userTier`**: `"development"` | `"free"` | `"premium"` -- always present
- **`license`**: `{ premiumKey, expiresAt, customer, status }` -- present only when `isPro` is `true`

### 4. `toggleWbCode` / `toggleWbCodeFile` -- Extended to PRO

**Files changed**: `WBC.js`

Guard changed from `if (__DEV__)` to `if (__DEV__ || isPro)`, making source code viewer toggles available to premium users.

### 5. Global Exposure -- Two-Level Architecture

**Files changed**: `WBC.js`

**Level 1 -- ALL users** (explicit `global` prop only):

```javascript
if (this.global_ || this.item_?.options?.global) {
    global[this.item_?.options?.global || this.global_] = this.itemAccessebility;
}
```

**Level 2 -- DEV only** (blanket exposure + `_vm`):

```javascript
if (__DEV__) {
    if (this.nameEl) {
        global[this.nameEl] = this.itemAccessebility;
        global[this.nameEl + "_vm"] = this;
    }
}
```

**Rationale**: Free/premium users who explicitly request global exposure via `global` prop should get it. Blanket exposure of all instances and raw Vue instances must remain dev-only.

### 6. Vuex Store: `_wbcProDetails`

**Files changed**: `store/index.js`

Added `state._wbcProDetails`, `mutations.setWbcProDetails`, `getters._wbcProDetails` for detailed license information.

### 7. Performance: Centralized Tier Detection

**Files changed**: `store/index.js`, `WBC.js`

- Added `isWbcPro` and `userTier` getters to the central store.
- Removed expensive per-component re-evaluation of license and tier status.
- Tier resolution is now O(1) via store getters. Significant performance boost when rendering large pages (4000+ components).

### 8. Feature Reclassification: `root` is now Premium

**Files changed**: `WBC.js`, `strategy/*`

`itemAccessebility.root` moved from Free to Premium. It provides direct access to `$store`, `$router`, and the full application tree -- an "Architect" feature, not a basic building block.

---

### Files Updated in This Cycle

| File | Update |
|---|---|
| `architecture_monetization_2026.md` | Added `__WBC_DEV__` docs, updated `__DEV__` definition, scenario matrix |
| `road_map_base_vs_premium.md` | Updated 3-Tier table, centralized logic docs, reclassified `root` |
| `release_blueprint.md` | Updated tier table, marked centralization as completed |
| `changelog_2026.md` | Created |

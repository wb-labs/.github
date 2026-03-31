# [PKG]: Item Accessibility & Utility Classification (Pattern)

> **Definition**: This document serves as the mandatory template for defining the public and private interface of a package's component items (`ctx` or `that` objects).

---

## 1. `ctx` Object Interface ([PKG] Interface)
Classify all exposed methods and properties by tier.

| Property / Method | Free | Premium (Pro) | Development (Dev) | Description |
|---|:---:|:---:|:---:|---|
| **Identity & Data** | | | | |
| `userTier` | ✅ | ✅ | ✅ | Returns 'Free', 'Premium', or 'Development'. |
| `name` | ✅ | ✅ | ✅ | The component's unique identifier. |
| `props` | ✅ | ✅ | ✅ | Access to component props. |
| `data` | ✅ | ✅ | ✅ | Reactive bridge to internal state. |
| `[Specific_Prop]` | [Tier] | [Tier] | [Tier] | [Description] |

| **Framework Hooks** | | | | |
| `vm` | ❌ | ✅ | ✅ | Raw Vue instance access (Pro). |
| `el` | ❌ | ✅ | ✅ | Raw DOM element access (Pro). |
| `emit` | ✅ | ✅ | ✅ | Event emission. |

---

## 2. Logic Injection & Orchestration Hooks
Define which lifecycle or orchestration hooks are available for each package.

| Hook | Free | Premium (Pro) | Dev Bypass | Description |
|---|:---:|:---:|:---:|---|
| `init(ctx)` | ✅ | ✅ | ✅ | Basic setup. |
| `logic(ctx)` | ❌ | ✅ | ✅ | Advanced orchestration (Pro). |
| `[Pkg_Hook]` | [Tier] | [Tier] | [Tier] | [Description] |

---

## 3. Utility Methods (Internal & Shared)
Document the specialized helpers used within the package.

| Utility Method | Category | Tier | Purpose |
|---|---|:---:|---|
| `[HelperName]` | [Logic] | [Tier] | [Description] |

---

## 4. Tiering Enforcement & Compilation
Every package MUST document its internal enforcement strategy:
*   **Build-Time**: Code stripping via Vite/Webpack flags.
*   **Runtime**: Dynamic gating in the `ctx` object constructor.
*   **Dev Bypass**: Full access when `__DEV__` is true.

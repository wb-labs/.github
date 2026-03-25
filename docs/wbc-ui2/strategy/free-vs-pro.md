# @wbc-ui2 — Free vs Pro: Complete Feature Comparison

> **"Free users can bind states. Pro users can command them."**
> **"3 hooks for builders, 7 hooks for architects."**

---

## The Open Core Model

WBC-UI2 keeps the **Renderer** free (driving adoption) while gating the **Orchestrator** and **Extractor** (monetizing business use cases).

---

## Component Interface (`itemAccessebility`)

Every WBC component exposes a controlled proxy called `itemAccessebility` (referred to as `that` in `dive` mode). What's available depends on your tier:

### Identity & Data

| Property / Method | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `userTier` | ✅ | ✅ | Returns `'Free'`, `'Premium'`, or `'Development'`. |
| `nameEl` | ✅ | ✅ | The global identifier or resolved component name. |
| `props` | ✅ | ✅ | The raw Vue props of the WBC instance. |
| `data` | ✅ | ✅ | **Reactive bridge** to the component's internal state. |
| `license` | ❌ | ✅ | The validated license object from store. |
| `data0` | ❌ | ✅ | Access to the original, non-reactive component definition. |
| `vm` | ❌ | ✅ | **Raw Vue Instance** for deep architectural access. |

### State Management

| Property / Method | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `update(v)` | ✅ | ✅ | Forces a component update cycle. |
| `emit(ev, val)` | ✅ | ✅ | Emits Vue events. |
| `get(key)` | ❌ | ✅ | Explicitly get a data property. |
| `set(val, key)` | ❌ | ✅ | Explicitly set a data property. |
| `val(v)` | ❌ | ✅ | High-level value getter/setter with validation. |

### Tiered Toggles

| Toggle | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `toggleLoad(v)` | 🔄 Binary | 🎯 Precision | Controls the Loading overlay. |
| `toggleProtected(v)` | 🔄 Binary | 🎯 Precision | Controls the Restricted Access overlay. |
| `toggleFloat(v)` | 🔄 Binary | 🎯 Precision | Toggles Floating/Absolute positioning. |
| `toggleClose(v)` | 🔄 Binary | 🎯 Precision | Toggles the Close button visibility. |
| `toggleDrag(v)` | 🔄 Binary | 🎯 Precision | Toggles Draggable state. |
| `toggleHide(v)` | 🔄 Binary | 🎯 Precision | Toggles conditional rendering. |

### Framework Access

| Property / Method | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `root` | ❌ | ✅ | The root Vue instance. |
| `store` | ❌ | ✅ | Access to Vuex store instance. |
| `router` | ❌ | ✅ | Access to Vue Router instance. |
| `routes` | ❌ | ✅ | Dictionary of all registered routes. |
| `routeParams` | ❌ | ✅ | Current URL parameters. |
| `ref(name)` | ❌ | ✅ | Access to child components via `$refs`. |
| `el` | ❌ | ✅ | Access to the raw DOM element. |
| `watch(p, cb)` | ❌ | ✅ | Dynamic property watcher. |

### Logic & Services

| Property / Method | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `dayjs` | ⚠️ ±14d | ✅ Full | Date manipulation utility. |
| `storage` | ⚠️ Basic | ✅ Full | LocalStorage bridge. |
| `cookies` | ⚠️ Basic | ✅ Full | Browser cookies bridge. |
| `markdown` | ❌ | ✅ | Bi-directional MD/HTML transformation. |
| `aes` (Enc/Dec) | ❌ | ✅ | Enterprise AES-256 encryption utilities. |
| `queryData` | ❌ | ✅ | High-level API fetcher with cache logic. |
| `trigger(method)` | ❌ | ✅ | Execute any public component method by name. |

---

## Logic Injection Hooks

WBC supports dynamic logic injection via `@wbc-logic` files or JS module exports.

| Hook | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `init0(ctx)` | ✅ | ✅ | Early setup (essential). |
| `init(ctx)` | ✅ | ✅ | Post-mount initialization. |
| `updater(ctx)` | ✅ | ✅ | Sync callbacks (consistency). |
| `setup(ctx)` | ❌ | ✅ | Module-level setup. |
| `tracker(ctx)` | ❌ | ✅ | Per-render orchestration. |
| `logic(ctx)` | ❌ | ✅ | General module logic injection. |
| `@wbc-logic` (Func) | ❌ | ✅ | Pure function injection. |
| **`output` (Prop)** | ❌ | ✅ | **God Mode Layout**: Transform VNode output. |

---

## Feature Categories Summary

| Feature Category | Free (Foundation) | Premium (Pro/Enterprise) |
| :--- | :--- | :--- |
| **Rendering** | Strings, Objects, Lists, Files | + Encrypted Configs, Remote Logic |
| **File Parsing** | Standard MD, JSON, TXT, JS | + Pipe Overrides (`\|`), Explicit Parser |
| **API (`that`)** | Standard UI Toggles, `data` | + `vm`, `data0`, `content` (Headless Extraction) |
| **Lifecycle** | 3 hooks for Builders | + 4 hooks for Architects (7 total) |
| **Form Engine** | Basic inputs | + `val`, `isValid`, `isValidFn` |
| **Dev Tools** | N/A | `wbCode`, `wbCodeFile` (Dev only) |

---

## Utility Functions Tiering

| Utility Type | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| **Daily Helpers** | ✅ | ✅ | `randomKey`, `capitalize`, `isDate`, `isEmpty`, etc. |
| **Time-Savers** | ❌ | ✅ | `mergeObjects`, `getObjectDepth`, `clone` |
| **Enterprise Security** | ❌ | ✅ | `aesEnc`, `aesDec` (physically stripped from free builds) |

---

## Getting a Pro License

Pro licenses are available for individual developers and enterprise teams:

- **Indie Developer**: One-time license for personal projects.
- **Enterprise**: Per-project license with priority support.

Visit [wbc-ui.com](https://wbc-ui.com) for pricing and activation.

# wb-core: Technical Reference

> Merged from: `technical/wb-core_file_handling_guide.md`, `technical/wb-core_item_accessibility_levels.md`, `technical/BUILD_OPTIMIZATION.md`, `technical/BUILD_SIZE_REPORT.md`, `technical/wb-core_ressource.md`, `strategy/wb-core_ressource.md`

---

## 1. File Handling

WBC employs heuristic detection to decide how to render JavaScript, TypeScript, and other file types.

### JS/TS Detection Flow

```
WBC receives .js/.ts path
  |
  +-- Phase 1: Source Text Check
  |     +-- Matches Vue pattern (export default + render/setup/template) --> Case 1: Vue Component
  |     +-- Contains @wbc-logic --> Case 6: Logic Provider
  |     +-- Otherwise --> Phase 2: Module Export Check
  |
  +-- Phase 2: Module Export Check
        +-- Exports init/setup/tracker/logic --> Case 6: Logic Provider
        +-- Exports POJO Object --> Case 3: Object Mapping
        +-- Exports Function --> Case 4: Function Source
        +-- None of above --> Case 2: Classic Script Snippet
```

### Case 6: Logic Provider (Tiered Execution)

The most powerful extension point. Triggered by the `@wbc-logic` marker or specific function exports.

| Hook | Tier | Purpose |
|---|---|---|
| `init(ctx)` | Free | Basic initialization (runs for all users) |
| `setup(ctx)` | Pro | Module-level architecture configuration |
| `tracker(ctx)` | Pro | Reactive orchestration on every render cycle |
| `logic(ctx)` | Pro | General runtime logic injection |

**Developer bypass**: In development mode (`serve_vite`), all hooks execute regardless of license.

### Pipe Syntax (Pro Feature)

Format: `item="[FilePath] | [CSS_Classes] | [Link_URL] | [Explicit_Parser]"`

Supported parsers: `md`, `tex`, `python`, `js`, `html`, `json`, `txt`.

```html
<!-- Render a .md file as a JS code snippet -->
<WBC item="./info.md|||js" />
```

### Programmatic Content Layer (Pro Feature)

Premium users access `ctx.content` for headless extraction:

```javascript
{
  input: {
    file: { js: "...", html: "...", md: "..." },
    item: "./sample.md"
  },
  output: {
    html: { pureHtml: "..." },
    md: { pureMd: "..." },
    vNodes: { main: VNode, wbCode: VNode }
  }
}
```

The `output` property allows Premium users to pass a custom configuration where string keys resolve to actual VNodes from `this.vNodes`, enabling full layout orchestration.

---

## 2. itemAccessebility (ctx) -- Complete Tiering Reference

### Identity & Data

| Property | Free | Pro | Dev | Description |
|---|:---:|:---:|:---:|---|
| `userTier` | Yes | Yes | Yes | Returns 'Free', 'Premium', or 'Development' |
| `license` | No | Yes | Yes | Validated license object from store |
| `nameEl` | Yes | Yes | Yes | Global identifier or resolved component name |
| `props` | Yes | Yes | Yes | Raw Vue props of the WBC instance |
| `data` | Yes | Yes | Yes | Reactive bridge to internal state |
| `data0` | No | Yes | Yes | Original non-reactive component definition |
| `vm` | No | Yes | Yes | Raw Vue instance for deep access |

### State Management

| Property | Free | Pro | Dev | Description |
|---|:---:|:---:|:---:|---|
| `get(key)` | No | Yes | Yes | Get a data property (defaults to `item_`) |
| `set(val, key)` | No | Yes | Yes | Set a data property (defaults to `item_`) |
| `val(v)` | No | Yes | Yes | High-level value getter/setter with validation |
| `update(v)` | Yes | Yes | Yes | Force a component update cycle |

### Toggles

All toggles exist at every tier. Free users get binary (on/off) control; Pro/Dev users get precision control (specific state values).

| Toggle | Free | Pro/Dev |
|---|---|---|
| `toggleLoad`, `toggleProtected`, `toggleFloat`, `toggleClose`, `toggleDrag`, `toggleHide` | Binary | Precision |
| `toggleWbCode`, `toggleWbCodeFile` | No | Dev only |

### Framework Access

| Property | Free | Pro | Dev | Description |
|---|:---:|:---:|:---:|---|
| `root` | No | Yes | Yes | Root Vue instance (`$store`, `$router`, full app tree) |
| `store` | No | Yes | Yes | Vuex store instance |
| `router` | No | Yes | Yes | Vue Router instance |
| `routes` | No | Yes | Yes | Dictionary of all registered routes |
| `routeParams` | No | Yes | Yes | Current URL parameters |
| `ref(name)` | No | Yes | Yes | Child components via `$refs` |
| `el` | No | Yes | Yes | Raw DOM element |
| `emit(ev, val)` | Yes | Yes (Raw) | Yes (Raw) | Vue event emitter |
| `watch(p, cb)` | No | Yes | Yes | Dynamic property watcher |

### Logic & Services

| Property | Free | Pro | Dev | Description |
|---|:---:|:---:|:---:|---|
| `dayjs` | +/-14d | Full | Full | Date manipulation |
| `storage` | Basic | Full | Full | LocalStorage bridge |
| `cookies` | Basic | Full | Full | Browser cookies bridge |
| `markdown` | No | Yes | Yes | Bi-directional MD/HTML transformation |
| `aes` | No | Yes | Yes | AES-256 encryption/decryption |
| `queryData` | No | Yes | Yes | API fetcher with cache logic |
| `trigger(method)` | No | Yes | Yes | Execute any public component method by name |

### Tiering Enforcement

- **Build-time**: Vite plugin removes `@destination: Pro` blocks from non-PRO production builds.
- **Runtime**: `itemAccessebility` computed property checks `isWbcPro || __DEV__` before attaching sensitive methods.
- **Dev bypass**: `__DEV__` (via `serve_vite`) grants full access regardless of license.

---

## 3. Internal Utility Methods

| Method | File | Tier | Purpose |
|---|---|:---:|---|
| `aesEnc` | `utils_pro.js` | Pro | AES-256 encryption (stripped in Free) |
| `aesDec` | `utils_pro.js` | Pro | AES-256 decryption (stripped in Free) |
| `safeEval` | `utils.js` | Pro | Secure expression evaluator |
| `strToObj` | `utils.js` | Dev | Turns strings into living objects/code |
| `cleanAggressive` | `utils_pro.js` | Pro | UI-focused HTML sanitizer |
| `randomColor` | `utils.js` | Free | Random hex code generator |
| `randomKey` | `utils.js` | Free | Collision-proof unique key generator |
| `capitalizeWords` | `utils.js` | Free | String formatter for auto-labeling |
| `isVnode` | `utils.js` | Free | Vue metadata detection |
| `isDate` | `utils.js` | Free | Strict date format validation |

---

## 4. Build Variants & Size Report

### Summary (as of 2026-02-07)

| Variant | Command | UMD Size | Gzipped | Use Case |
|---|---|---|---|---|
| **Standard** | `npm run build` | 175 KB | 49 KB | Production apps with managed deps |
| **With-Prettier** | `npm run build:with-prettier` | ~1,400 KB | ~400 KB | Convenience (code formatting built-in) |
| **Full-Embed** | `npm run build:full-embed` | 7,772 KB | ~2.6 MB | Quick demos, CDN usage, minimal setup |

The standard build achieved an **87% size reduction** (from 1.4 MB) by externalizing Prettier and other optional dependencies.

### Externalization Strategy

```javascript
// vite.config.js (simplified)
external: (id) => {
    if (isFullEmbed) {
        // Only externalize: vue, prettier/*, @guolao/vue-monaco-editor
    } else if (isWithPrettier) {
        // Bundle Prettier, externalize UI frameworks + optional libs
    } else {
        // Standard: externalize everything
    }
}
```

### What Each Build Bundles

**Standard** (recommended for production):
- Core WBC logic, markdown-it, lz-string, vue-json-viewer, turndown, vue-cookies, vue-cryptojs
- User must install: `vue`, `vuetify`, `bootstrap-vue` (optional: `prettier`, `echarts`, `leaflet`, `mermaid`, `codemirror`)

**Full-Embed** (for CDN/demos):
- Vuetify (~5-6 MB), Bootstrap-Vue (~1 MB), Leaflet (~500 KB), Prism (~300 KB), core logic (~300 KB)
- Externalizes only: Vue, Prettier (~1.2 MB), Monaco (~5-6 MB)

### Load Time Comparison (3G)

| Build | Gzipped | Load Time |
|---|---|---|
| Standard | 49 KB | ~0.3s |
| With-Prettier | ~400 KB | ~2.5s |
| Full-Embed | 2.6 MB | ~17s |

### Peer Dependencies

- **Required**: `vue` (^2.7.0), `vuetify` (^2.7.0), `vuex` (^3.6.0), `vue-router` (^3.5.0)
- **Optional**: `prettier`, `echarts`, `leaflet`, `mermaid`, `codemirror`, `@guolao/vue-monaco-editor`, `pdfjs-dist`, `highlight.js`

All optional deps are marked in `peerDependenciesMeta`, so npm only warns when a feature that needs them is used.

---

## 5. Resources & URLs

### Packages & Repos

| Resource | URL |
|---|---|
| npm Package | https://www.npmjs.com/package/wbc-ui2 |
| Core Source | https://github.com/nicofr83/wbc-ui2/tree/main/wb-core |
| Core Issues | https://github.com/nicofr83/wbc-ui2/issues?q=label%3Awb-core |
| Template (Vite) | https://github.com/nicofr83/wbc-ui2/tree/main/apps/wb-core_template_vite |
| Template (Vue CLI) | https://github.com/nicofr83/wbc-ui2/tree/main/apps/wb-core_template_cli |
| Template (Webpack) | https://github.com/nicofr83/wbc-ui2/tree/main/apps/wb-core_template_webpack |

### Live Sites

| Resource | URL |
|---|---|
| Main Site | https://wbc-ui.com |
| Markdown Documentation | https://md.wbc-ui.com |
| Routing Documentation | https://wbRoutes2.wbc-ui2.com |

### Validation Flow

```
wb-core/src/  <-- THE SOURCE OF TRUTH
    |
    v
  1. wb-core_demo/          (validate: does the code work?)
    |
    v
  2. wbc-ui.com/            (document: what does it do?)
    |
    v
  3. md.wbc-ui.com/         (showcase: markdown features)
    |
    v
  4. wbRoutes2.wbc-ui2.com/ (showcase: routing patterns)
```

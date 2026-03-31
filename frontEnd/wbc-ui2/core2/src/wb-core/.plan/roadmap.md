# wb-core: Roadmap

> Merged from: `strategy/wb-core_roadmap.md`, `strategy/wb-core_release_blueprint.md`, `strategy/wb-core_blueprint_wbc3_vision.md`

---

## Prerequisites

- [X] Logged into NPM (`npm login`)
- [ ] GitHub Organization `wbc-ui` created

---

## Phase 1: NPM Publication (The Engine)

1. Enter `wb-core/`, verify `package.json` version is `0.0.1`.
2. Publish: `npm publish --access public`

---

## Phase 2: Documentation & Apps Deployment

| App | Source | Deploy Target | Purpose |
|---|---|---|---|
| Main docs (VuePress) | `apps/wb-core_wbc-ui.com/` | `https://wbc-ui.com` | API reference, component guides, live `<WBC>` rendering |
| Markdown demo | `apps/wb-core_md.wbc-ui.com/` | `https://md.wbc-ui.com` | `<WBC item="./file.md"/>` file rendering showcase |
| Routing demo | `apps/wb-core_wbRoutes2.wbc-ui2.com/` | `https://wbRoutes2.wbc-ui2.com` | WBC as Vue Router component, multilingual/encrypted routing |

---

## Phase 3: Ecosystem Deployment (Templates & Demo)

> Before pushing templates, switch all `file:` local paths in `package.json` back to npm version ranges.

| Artifact | Repo |
|---|---|
| Demo app | `wbc-ui/wbc-ui2-demo` |
| Template (Vite) | `wbc-ui/wbc-ui2-template-vite` |
| Template (Vue CLI) | `wbc-ui/wbc-ui2-template-cli` |
| Template (Webpack) | `wbc-ui/wbc-ui2-template-webpack` |

---

## Phase 4: Marketing Execution

| Platform | Source folder |
|---|---|
| Dev.to | `wbc-ui.com_marketing/wbc-ui.com_devToBoost/` |
| LinkedIn | `wbc-ui.com_marketing/wbc-ui.com_linkedInBoost/` |
| GitHub Org README | `wbc-ui.com_marketing/wbc-ui.com_githubBoost/` |
| Twitter/X | `wbc-ui.com_marketing/wbc-ui.com_twitterBoost/` |
| Reddit | `wbc-ui.com_marketing/wbc-ui.com_redditBoost/` |

---

## Phase 5: Verification

- [ ] `npm install wbc-ui2` works in a clean environment
- [ ] All GitHub template repos are buildable
- [ ] Docs live at `https://wbc-ui.com`
- [ ] Markdown app live at `https://md.wbc-ui.com`
- [ ] Routing app live at `https://wbRoutes2.wbc-ui2.com`

---

## Release Blueprint: 3-Tier Build Model

Before each release, enforce the following constants:

| Tier | Build Flag | `userTier` | Access Level |
|---|---|---|---|
| DEV | `__WBC_DEV__ = true` | `"development"` | Everything: Free + Pro + developer tools |
| FREE | `__WBC_PRO__ = false` | `"free"` | Standard: core UI, basic toggles, i18n, limited `dayjs` |
| PRO | `__WBC_PRO__ = true` | `"premium"` | Architect: full orchestration, `vm`, `store`, `router`, encryption |

### Pre-release checklist

- [ ] `__WBC_PRO__` set correctly per variant (`true` for Pro, `false` for Free)
- [ ] `__WBC_DEV__` is `false` in production (disables `window.elm`, blanket `_vm` leaks)
- [ ] `_originalItem` stores original file path for `wbCode`
- [ ] `toggleWbCode` / `toggleWbCodeFile` cycle correctly (3-state)
- [ ] Template `package.json` files use npm ranges, not `file:` paths

### Customer Onboarding

```javascript
import WbcUi from 'wbc-ui2';

Vue.use(WbcUi, {
  premiumKey: 'YOUR_LICENSE_KEY',
  lg: 'en'
});
```

License keys (16-char, e.g. `ABCD-1234-EFGH-5678`) are delivered via LemonSqueezy/Gumroad. Validation is cached for 24 hours; fail-open ensures production apps are never blocked by network issues.

---

## Version History

### v0.0.1 -- Foundation

- [X] WBC render engine (strings, arrays, objects)
- [X] Extended install system
- [X] File rendering (served, online, local)
- [X] Media detection (image, video, audio, PDF)
- [X] Hover states, trackers, global mapping
- [X] Markdown rendering via MarkdownIt
- [X] Vite build configuration
- [X] Demo, Markdown, and Routing apps
- [X] Templates for Vite, Vue CLI, and Webpack
- [X] VuePress documentation site

### v0.1.0 -- Modularization

- [X] Extract Leaflet to `@wbc-ui2/gis`
- [X] Extract VueOffice to `@wbc-ui2/office`
- [ ] Extract bootstrap-vue dependency (optional)
- [ ] TypeScript type definitions
- [ ] Reduce `extended_install.js` footprint

### v0.2.0 -- Enhanced Features

- [ ] Improved error boundaries for invalid items
- [ ] Lazy-load extension packages
- [ ] Plugin system for custom renderers
- [ ] SSR compatibility

### v1.0.0 -- Stable Release

- [X] Full API documentation coverage
- [X] Advanced file parsing (`parsedAs` overrides)

---

## WBC-UI3 Vision: TypeScript & Vue 3 Migration

> Goal: Transition from JS/Vue 2 to a type-safe Vue 3 ecosystem while preserving the "One-Object" architecture.

### Architecture Shift

Replace the monolithic `WBC.js` with Composition API composables:

```
/src
  /composables
    useWbcMeta.ts          # nameEl, key, options resolution
    useWbcPermissions.ts   # Pro/Free/Dev logic
    useWbcRender.ts        # The toWBC_ engine (VNode generation)
    useWbcAccessibility.ts # Building the "that" object
  WBC.vue                  # Entry point using <script setup>
```

### Key TypeScript Interfaces

```typescript
interface WbcItem {
  comp?: string | Component;
  title?: string;
  options?: WbcOptions;
  children?: WbcItem[];
  init?: (that: ItemAccessibility) => void;
  tracker?: (that: ItemAccessibility) => void;
  logic?: (that: ItemAccessibility) => void;
}

interface ItemAccessibility {
  userTier: 'free' | 'premium' | 'development';
  data: any;
  props: Record<string, any>;
  emit: (event: string, ...args: any[]) => void;
  root?: any;   // Premium only
  vm?: any;     // Premium only
  store?: any;  // Premium only
}
```

### Vue 3 Performance Gains

- **Proxy-based reactivity**: Handle 10,000+ nested objects without lag (replaces `Object.defineProperty`)
- **Fragments**: Multiple root nodes simplify `wrap_` logic
- **Tree-shaking**: `__WBC_PRO__` via Vite `define` + dynamic imports strip Pro code from Free builds

### Migration Phases

| Phase | Timeline | Goal |
|---|---|---|
| 1. Typing | Month 1 | Ship `.d.ts` for the Vue 2 version as a "Pro Bonus" |
| 2. Composable refactor | Month 2 | Extract `itemAccessebility` into a standalone TS function, test with Vitest |
| 3. Vue 3 bridge | Month 3 | Use `vue-demi` for dual Vue 2/3 support, finalize `h()` differences |

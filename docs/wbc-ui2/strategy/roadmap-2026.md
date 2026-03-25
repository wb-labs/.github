# WBC-UI2 Strategic Roadmap (2026–2027)

## 🎯 The Vision

To transform **WBC-UI2** from a specialized internal library into the definitive **Low-Code Operating System for the Vue Ecosystem**, targeting Developer Experience (DX) and Enterprise efficiency gaps.

---

## 📅 Phase 1: The Vue 2 "Professional" Era (Q1 – Q2 2026)

**Primary Goal**: Stabilize the library and serve the Vue 2 user base.

### Milestones
- ✅ Centralized Licensing — LemonSqueezy integration with persistent cookie-based caching.
- ✅ Developer Capability Gate — `vm`, `refs`, `data0` isolated as premium-only.
- ✅ 5 Packages Published — `wbc-ui2`, `@wbc-ui2/code`, `chart`, `latex`, `mermaid`.
- ✅ Public Website & Docs — [wbc-ui.com](https://wbc-ui.com) launched.
- 🚧 Interactive Lab — Live playground at wbc-ui.com.
- 🟡 Remaining Packages — `@wbc-ui2/table`, `@wbc-ui2/gis`, `@wbc-ui2/wbDataviewer`.

---

## 🚀 Phase 2: The Vue 3 & TypeScript Revolution (Q3 – Q4 2026)

**Primary Goal**: Future-proof the product for the modern Vue ecosystem.

### Milestones
- Full Vue 3 Conversion — Rewrite core using Composition API.
- TypeScript First — Native, deep types for the entire ecosystem.
- WBC Presets — `preset="admin"` or `preset="doc"` for instant boilerplate-less apps.
- Performance — Proxy-based reactivity for 10,000+ nested object models.

### New Module Structure (Planned)
```
/src
  /composables
    useWbcMeta.ts           # Resolving nameEl, key, options
    useWbcPermissions.ts    # Pro/Free/Dev logic
    useWbcRender.ts         # The rendering engine
    useWbcAccessibility.ts  # Building the `that` object
  WBC.vue                   # Entry point using <script setup>
```

### Key TypeScript Interfaces (Planned)
```typescript
interface WbcItem {
  comp?: string | Component;
  title?: string;
  options?: WbcOptions;
  children?: WbcItem[];
  init?: (that: ItemAccessibility) => void;
  tracker?: (that: ItemAccessibility) => void;
}

interface ItemAccessibility {
  userTier: 'free' | 'premium' | 'development';
  data: any;
  props: Record<string, any>;
  emit: (event: string, ...args: any[]) => void;
  // Premium only
  root?: any;
  vm?: any;
  store?: any;
}
```

---

## 🌐 Phase 3: The Platform & SaaS (2027)

**Primary Goal**: Achieve market dominance in the Low-Code Vue niche.

### Milestones
- **Component Store** — Developers build and sell WBC-compatible plugins.
- **Visual Builder** — Drag-and-drop interface generating WBC JSON structures.
- **CI/CD Integration** — Automatic license validation for GitHub Actions/Vercel.

---

## 🛡️ Key Risks & Mitigation

| Risk | Mitigation |
| :--- | :--- |
| Competition from large players | Stay hyper-niche: best at **dynamic data-driven components**, not generic layouts. |
| Vue 2 + Vue 3 maintenance burden | Shared core logic in pure JS/TS wrapped by version-specific packages. |

---

**Strategic Value Proposition**: *"WBC-UI2 is the bridge that keeps legacy projects alive and makes new projects buildable in hours instead of weeks."*

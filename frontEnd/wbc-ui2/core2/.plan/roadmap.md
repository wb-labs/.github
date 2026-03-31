# WBC-UI2 Strategic Roadmap (2026-2027)

> To transform WBC-UI2 from a specialized internal library into the definitive **Low-Code Operating System for the Vue Ecosystem**.

---

## Phase 1: The Vue 2 "Professional" Era (Q1-Q2 2026)

**Goal**: Stabilize the library and serve the Vue 2 user base.

| Milestone | Status | Notes |
|-----------|--------|-------|
| Centralized Licensing (LemonSqueezy + cookie caching) | Done | |
| Developer Capability Gate (`vm`, `refs`, `data0` as premium) | Done | |
| 5 Packages Published (`wbc-ui2`, `code`, `chart`, `latex`, `mermaid`) | Done | |
| Public Website & Docs ([wbc-ui.com](https://wbc-ui.com)) | Done | |
| Interactive Lab (live playground at wbc-ui.com) | In Progress | |
| Remaining Packages (`table`, `gis`, `wbDataviewer`) | Planned | |
| Security Hardening (DOMPurify, remove safeEval, CSP) | **Not Started** | Critical — see [audit.md](audit.md) |
| WBC.js refactor (split 5,750-line file into modules) | **Not Started** | High priority |

### Immediate Actions (Next 30 Days)
1. **Security**: Replace `safeEval()` with sandboxed evaluation. Add DOMPurify for all innerHTML assignments.
2. **Refactor**: Split WBC.js into focused modules (<500 lines each).
3. **Testing**: Set up Vitest, write first 20 unit tests for core rendering.
4. **CI/CD**: GitHub Actions pipeline for lint + test + build.

---

## Phase 2: The Vue 3 & TypeScript Revolution (Q3-Q4 2026)

**Goal**: Future-proof the product for the modern Vue ecosystem.

### Architecture Migration

| Current (Vue 2) | Target (Vue 3) |
|------------------|-----------------|
| Options API | Composition API (`<script setup>`) |
| Vuex 3 | Pinia |
| `Object.defineProperty` | `Proxy`-based reactivity |
| Single root required | Fragments (multiple roots) |
| Limited tree-shaking | Native ESM, full tree-shaking |
| Bootstrap-Vue | TBD (no Vue 3 port) |
| Vuetify 2 | Vuetify 3 (different API) |

### New Module Structure

```
/src
  /composables
    useWbcMeta.ts           # Resolving nameEl, key, options
    useWbcPermissions.ts    # Pro/Free/Dev logic
    useWbcRender.ts         # The rendering engine
    useWbcAccessibility.ts  # Building the `that` object
  WBC.vue                   # Entry point using <script setup>
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
  // Premium only
  root?: any;
  vm?: any;
  store?: any;
}
```

### Pro Guard System (Tree-Shakeable)

```typescript
const setupProFeatures = async (acc: ItemAccessibility) => {
  if (__WBC_PRO__) {
    const { attachProCapabilities } = await import('./pro/engine');
    attachProCapabilities(acc);
  }
}
```

### Milestones

| Milestone | Timeline | Priority |
|-----------|----------|----------|
| Publish JSON Schema specification for config format | Month 1 | Critical |
| TypeScript `.d.ts` for Vue 2 version (Pro bonus) | Month 1 | High |
| Move `itemAccessebility` into independent TS composables | Month 2 | High |
| `vue-demi` compatibility (both Vue 2 and Vue 3) | Month 3 | High |
| Full Vue 3 Composition API rewrite | Month 4-5 | Critical |
| WBC Presets (`preset="admin"`, `preset="doc"`) | Month 6 | Medium |
| Proxy-based reactivity for 10,000+ nested objects | Month 6 | Medium |

---

## Phase 3: The Platform & SaaS (2027)

**Goal**: Achieve market dominance in the Low-Code Vue niche.

### Milestones

| Milestone | Description |
|-----------|-------------|
| **One Killer Demo** | Interactive playground showing the "aha moment" in 30 seconds |
| **AI Integration Demo** | Claude/GPT API > WBC-UI2 renders live. The viral demo. |
| **Visual Config Builder** | Drag-and-drop editor outputting WBC-UI2 JSON (the Form.io model) |
| **Component Store** | Developers build and sell WBC-compatible plugins (15-30% commission) |
| **Framework-Agnostic Core** | Extract JSON interpretation from Vue. Support React, Svelte, Solid. |
| **Enterprise Pilot Program** | 3-5 companies using WBC-UI2 in production with documented case studies |
| **SSR/SSG Support** | Nuxt integration for SEO-critical use cases |
| **CI/CD Integration** | Automatic license validation for GitHub Actions/Vercel |

---

## Effort Estimates (Build vs Reality Gap)

| To Make It Viable | Estimated Effort |
|-------------------|------------------|
| Vue 3 migration (Vue 3, Vuetify 3, Pinia, Composition API) | 3-6 months full-time |
| Test suite (unit + integration, 60%+ coverage) | 2-3 months |
| WBC.js refactor (split into modules) | 2-4 weeks |
| Security hardening (DOMPurify, CSP, remove safeEval) | 1-2 weeks |
| JSON Schema specification + TypeScript types | 2-4 weeks |
| CI/CD pipeline | 1 week |
| Documentation consolidation | 2-4 weeks |
| Proper license server (not client-side cookie check) | 2-3 weeks |

**Total to production-grade:** ~6-12 months of focused engineering.

---

## Key Risks & Mitigation

| Risk | Severity | Mitigation |
|------|----------|------------|
| Vue 2 EOL (Dec 2023) | Critical | Vue 3 migration is existential. #1 priority. |
| Single contributor (bus factor = 1) | High | Build community, find co-maintainers |
| No TypeScript | High | Enterprise adoption requires type safety |
| Amis could expand West | Medium | Speed matters. Ship Vue 3 before they translate docs. |
| React dominance (50%+ market) | Medium | Framework-agnostic core or React adapter |
| Zero automated tests | High | Vitest setup, start with core rendering tests |

---

*Consolidated from: `strategy/roadmap-2026.md`, `strategy/vue3-vision.md`, `claude/wbc-ui2-audit-2026-03-30.md`, `claude/wbc-ui2-strategic-analysis-2026-03-30.md`*

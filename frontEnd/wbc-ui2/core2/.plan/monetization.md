# WBC-UI2 — Monetization & Free vs Pro Strategy

---

## The Open Core Model

WBC-UI2 keeps the **Renderer** free (driving adoption) while gating the **Orchestrator** and **Extractor** (monetizing business use cases).

> **"Free users can bind states. Pro users can command them."**
> **"3 hooks for builders, 7 hooks for architects."**

---

## 1. Value Proposition by Tier

### Free Tier (Public NPM)
- **Target**: General developers, open-source projects, curious builders
- **Features**: Core UI rendering, basic props, standard display
- **Limitations**: No advanced logic hooks, no premium exports, no deep system introspection
- **Purpose**: Drive adoption, build community, prove the concept

### Pro Tier (Paid/Private)
- **Target**: Professional engineers, enterprises, high-performance apps
- **Features**: Full logic hooks, premium toolbars (PDF/Excel), performance monitoring, headless extraction
- **Support**: Direct owner support, priority updates

---

## 2. Component Interface (`itemAccessebility`) — Tiered Access

### Identity & Data

| Property / Method | Free | Pro | Description |
|:---|:---:|:---:|:---|
| `userTier` | Y | Y | Returns `'Free'`, `'Premium'`, or `'Development'` |
| `nameEl` | Y | Y | Global identifier or resolved component name |
| `props` | Y | Y | Raw Vue props |
| `data` | Y | Y | Reactive bridge to internal state |
| `license` | - | Y | Validated license object from store |
| `data0` | - | Y | Original, non-reactive component definition |
| `vm` | - | Y | Raw Vue Instance (deep architectural access) |

### State Management

| Property / Method | Free | Pro | Description |
|:---|:---:|:---:|:---|
| `update(v)` | Y | Y | Force component update cycle |
| `emit(ev, val)` | Y | Y | Emit Vue events |
| `get(key)` | - | Y | Explicitly get a data property |
| `set(val, key)` | - | Y | Explicitly set a data property |
| `val(v)` | - | Y | High-level value getter/setter with validation |

### Tiered Toggles

| Toggle | Free | Pro |
|:---|:---:|:---:|
| `toggleLoad(v)` | Binary | Precision |
| `toggleProtected(v)` | Binary | Precision |
| `toggleFloat(v)` | Binary | Precision |
| `toggleClose(v)` | Binary | Precision |
| `toggleDrag(v)` | Binary | Precision |
| `toggleHide(v)` | Binary | Precision |

### Framework Access (Pro Only)

| Property / Method | Description |
|:---|:---|
| `root` | Root Vue instance |
| `store` | Vuex store instance |
| `router` | Vue Router instance |
| `routes` | Dictionary of registered routes |
| `routeParams` | Current URL parameters |
| `ref(name)` | Child components via `$refs` |
| `el` | Raw DOM element |
| `watch(p, cb)` | Dynamic property watcher |

### Logic & Services

| Property / Method | Free | Pro | Description |
|:---|:---:|:---:|:---|
| `dayjs` | Limited (+-14d) | Full | Date manipulation |
| `storage` | Basic | Full | LocalStorage bridge |
| `cookies` | Basic | Full | Browser cookies bridge |
| `markdown` | - | Y | Bi-directional MD/HTML transformation |
| `aes` (Enc/Dec) | - | Y | Enterprise AES-256 encryption |
| `queryData` | - | Y | High-level API fetcher with cache |
| `trigger(method)` | - | Y | Execute any public component method |

---

## 3. Logic Injection Hooks

| Hook | Free | Pro | Description |
|:---|:---:|:---:|:---|
| `init0(ctx)` | Y | Y | Early setup (essential) |
| `init(ctx)` | Y | Y | Post-mount initialization |
| `updater(ctx)` | Y | Y | Sync callbacks (consistency) |
| `setup(ctx)` | - | Y | Module-level setup |
| `tracker(ctx)` | - | Y | Per-render orchestration |
| `logic(ctx)` | - | Y | General module logic injection |
| `@wbc-logic` (Func) | - | Y | Pure function injection |
| **`output` (Prop)** | - | Y | **God Mode Layout**: Transform VNode output |

---

## 4. Feature Gating Implementation

All components MUST gate features using the unified store's `isPackageAuthorized` getter.

| Feature Type | Free Behavior | Pro Behavior |
|:---|:---|:---|
| **Toolbar Icons** | Hidden or "Pro Only" tooltip | Full interaction |
| **Logic Hooks** | Console warning: "Pro License Required" | Full execution |
| **Data Export** | Alert: "Upgrade for PDF Export" | Immediate file generation |

---

## 5. Distribution Mechanism

Each package produces two distinct builds to prevent license theft:

1. **Public Bundle**: Minified and stripped of all `if (__WBC_PRO__)` blocks. Safe for public NPM.
2. **Premium Bundle**: Full-featured, packaged as private `.tgz` or hosted on private registry.

### Build Scripts

```json
{
    "serve_vite":      "vite",                          // Owner mode
    "serve_vite:free": "cross-env WBC_PRO=false vite",  // Simulate Free
    "serve_vite:pro":  "cross-env WBC_PRO=true vite",   // Simulate Pro
    "build_vite:free": "cross-env WBC_PRO=false vite build",
    "build_vite:pro":  "cross-env WBC_PRO=true vite build --outDir dist-pro"
}
```

---

## 6. Pricing Strategy

### Competitive Landscape

| Product | Pricing Model |
|---------|---------------|
| Vuetify Enterprise | ~$500/dev/year |
| PrimeVue | $99-$249/year |
| FormKit Pro | $129/year |
| Syncfusion (Vue) | $995/dev/year |
| Form.io Enterprise | $25K-100K+/year |

### Recommended WBC-UI2 Pricing

| Tier | Price | Target |
|------|-------|--------|
| **Indie Developer** | $49-79 one-time (or $29/year) | Solo devs, side projects |
| **Small Team (2-5)** | $149-249/year | Startups, small teams |
| **Enterprise** | $499-799/year per project | Companies, agencies |

Start low to build trust. First 50 paying customers matter more than maximizing per-seat revenue.

### Enterprise ROI Justification

| Without WBC-UI2 | With WBC-UI2 |
|:---|:---|
| 5 frontend devs at $130K = $650K/year | 2 devs + 3 config editors at $70K = $470K/year |
| UI change = PR + deploy (2-5 days) | Config change = instant (minutes) |
| White-label: fork per client | One codebase, one JSON config per client |

---

## 7. Go-to-Market Playbook

### Phase 1: Developer Adoption
- Open-source core (MIT license) — free forever
- npm installable, works in existing projects
- Target: individual developers and small teams
- Metric: npm downloads, GitHub stars

### Phase 2: Team Adoption
- Teams hit free tier limitations
- Self-serve upgrade to Pro ($20-50/user/month)
- Target: startup and mid-market engineering teams
- Metric: Pro conversions, team size

### Phase 3: Enterprise Sales
- Bottom-up discovery through developer adoption
- Needs: SSO, audit logging, SLA, custom integrations
- Enterprise tier: $25K-100K+/year (custom pricing)
- Metric: ACV (annual contract value)

---

*Consolidated from: `strategy/free-vs-pro.md`, `strategy/pkg_monetization_strategy.md`, `claude/wbc-ui2-strategic-analysis-2026-03-30.md`, `claude/project-assessment-2026-03-31.md`*

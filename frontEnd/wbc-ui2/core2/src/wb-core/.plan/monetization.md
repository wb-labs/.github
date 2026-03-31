# wb-core: Monetization & Licensing

> Merged from: `strategy/wb-core_monetization.md`, `technical/wb-core_licensing_flow.md`, `technical/wb-core_architecture_monetization_2026.md`

---

## 1. The Open Core Model

The **Renderer** is free (drives adoption). The **Orchestrator** and **Extractor** are premium (drives revenue).

### Value by Tier

| Capability | Free (Public NPM) | Pro (Licensed) |
|---|---|---|
| UI rendering (strings, arrays, objects, files) | Yes | Yes |
| State toggles (hide, float, drag, close) | Binary toggles | Precision control |
| i18n, form support, auth-aware | Yes | Yes |
| Basic lifecycle (`init0`, `init`, `updater`) | Yes | Yes |
| `dayjs` date utilities | Limited (plus/minus 14 days) | Full range |
| Storage / cookies | Basic | Full |
| God Mode API (`vm`, `refs`, `data0`, `trigger`) | No | Yes |
| Content extraction pipeline (`content`) | No | Yes |
| Advanced lifecycle (`tracker`, `watch`, `logic`, `setup`) | No | Yes |
| Store, router, routes access | No | Yes |
| AES encryption/decryption | No | Yes |
| Code inspection (`wbCode`, `wbCodeFile`) | No | Dev only |
| Pipe syntax file overrides (`parsedAs`) | No | Yes |
| `output` property (dynamic layout orchestration) | No | Yes |

### Distribution

| Package | Tier | Notes |
|---|---|---|
| `@wbc-ui2/core` | Free | Standard public release |
| `@wbc-ui2/core-pro` | Premium | Paywalled release for licensed customers |

The `pkg` slug in the store's `tiers` object is **`core`**.

---

## 2. Licensing Flow

### Trigger: `created()` in `WBC.js`

1. Check for existing cookie (`_wb_core_auth`).
2. If found and valid (under 24h old), hydrate the store's `tiers.core` state.
3. If not found and a `premiumKey` was passed during `Vue.use()`:
   - If key is `WBC_SIMULATE_PRO`, authorize immediately (simulation mode).
   - Otherwise, validate against the LemonSqueezy API.
4. Commit `status` and `details` to the store.

### Persistence

| Parameter | Value |
|---|---|
| Cookie name | `_wb_core_auth` |
| Store slug | `core` |
| Max age | 86400 (24 hours) |
| Mode | `SameSite=Lax` |

### Store Configuration

```javascript
// wb-core/src/store/index.js
state: {
  _wbcDev: __WBC_DEV__,
  tiers: {
    core: {
      authorized: !!detectLicense(),
      details: null
    }
  }
}
```

Legacy getters for backward compatibility:
- `_wbcProAuthorized` maps to `tiers.core.authorized`
- `_wbcProDetails` maps to `tiers.core.details`

### Gating Logic in `WBC.js`

```javascript
const isAuthorized = this.isWbcPro || __DEV__;

if (isAuthorized) {
    if (mod.setup) mod.setup(ctx);
    if (mod.tracker) mod.tracker(ctx);
    if (mod.logic) mod.logic(ctx);
} else {
    console.warn("[WBC-UI2] Advanced JS features require a PRO license.");
}
```

### Feature Locking Summary

| Feature | Free | Pro | Dev |
|---|---|---|---|
| `ctx.vm`, `ctx.proto`, `ctx.root` | Blocked | Yes | Yes |
| `ctx.markdown.md2Html`, `ctx.aes.enc` | Blocked | Yes | Yes |
| `ctx.dayjs` | +/-14 days | Unlimited | Unlimited |
| `setup`, `tracker`, `logic` hooks | Blocked | Yes | Yes |

---

## 3. Technical Protection

### Symbol-based Hiding

```javascript
const _PRO_EXTRACTOR = Symbol('wbc_pro_content');
const _INTERNAL_VM = Symbol('wbc_vm_instance');

this.itemAccessibility[_INTERNAL_VM] = this;
// Not visible in Object.keys() or console.log()
```

### Build-time Stripping

The Vite plugin removes `@destination: Pro` blocks during non-PRO production builds. Even if code exists at runtime, `itemAccessebility` checks `isWbcPro || __DEV__` before attaching sensitive methods.

### Monitoring

- **Graceful fail-open**: If the license server is unreachable, the library stays functional but logs a warning. Legitimate users are never blocked in production.
- **24-hour cache**: Licenses are cached to ensure seamless offline work.

---

## 4. Pricing Model

| License Type | Price | Target |
|---|---|---|
| Developer License | $49-$149 | Individual developers |
| Enterprise Site License | $2,000+ | Organizations |

Delivered via LemonSqueezy/Gumroad. Key format: 16-character (e.g. `ABCD-1234-EFGH-5678`).

---

## 5. Revenue Projections

| Scenario | Annual Revenue |
|---|---|
| Small success (200 licenses/year) | $10,000-$30,000 |
| Large success (standard for internal tools) | $100,000+ (licenses + consulting) |
| Consulting rate (as library author) | $150-$250/hour |

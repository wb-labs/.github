# WBC-UI2 — Free vs Pro: What Do You Get?

## The Philosophy

> **"Free users can build. Pro users can orchestrate."**

The free tier gives you everything you need to render dynamic UIs from JSON. The Pro tier unlocks the full power of the orchestration engine — advanced lifecycle hooks, framework-level access, and enterprise utilities.

---

## At a Glance

| Capability | Free | Pro |
|:---|:---:|:---:|
| JSON-to-UI rendering | Yes | Yes |
| String, Object, Array, File rendering | Yes | Yes |
| Vuetify + Bootstrap component support | Yes | Yes |
| i18n (en, fr, ar) | Yes | Yes |
| Basic lifecycle hooks (init, updater) | Yes | Yes |
| Markdown rendering | Yes | Yes |
| Form validation (basic) | Yes | Yes |
| | | |
| Advanced hooks (setup, tracker, logic) | - | Yes |
| Framework access (store, router, refs) | - | Yes |
| Raw Vue instance access | - | Yes |
| Headless content extraction | - | Yes |
| AES-256 encryption | - | Yes |
| Advanced API fetcher with caching | - | Yes |
| Dynamic property watchers | - | Yes |
| Full date manipulation | - | Yes |
| God Mode Layout (VNode transform) | - | Yes |
| Priority support | - | Yes |

---

## Lifecycle Hooks — 3 for Builders, 7 for Architects

### Free (3 hooks)

```javascript
{
  comp: 'v-card',
  init0(that) { /* Early setup */ },
  init(that)  { /* Post-mount initialization */ },
  updater(that) { /* Sync callbacks */ }
}
```

### Pro (7 hooks)

```javascript
{
  comp: 'v-card',
  init0(that) { /* Early setup */ },
  init(that)  { /* Post-mount */ },
  updater(that) { /* Sync */ },
  setup(that) { /* Module-level setup */ },
  tracker(that) { /* Per-render orchestration */ },
  logic(that) { /* General logic injection */ },
  output(h, vnode) { /* Transform the rendered output */ }
}
```

---

## The `that` Object — Tiered Access

Every component exposes a controlled proxy. What's available depends on your tier:

### Always Available (Free)

```javascript
that.userTier    // 'free' | 'premium' | 'development'
that.nameEl      // Component identifier
that.props       // Vue props
that.data        // Reactive state bridge
that.emit(event, value)  // Event emission
that.update()    // Force re-render
```

### Pro Unlocks

```javascript
that.vm          // Raw Vue instance
that.root        // Root app instance
that.store       // Vuex store
that.router      // Vue Router
that.routes      // All registered routes
that.ref('name') // Child component access
that.el          // Raw DOM element
that.watch(prop, callback)  // Dynamic watchers
that.get(key)    // Explicit data getter
that.set(val, key)  // Explicit data setter
that.val(v)      // High-level getter/setter with validation
that.markdown    // MD/HTML transformation
that.aes         // AES-256 encryption
that.queryData   // API fetcher with caching
that.trigger(method)  // Execute component methods
```

---

## Toggle Precision

Both tiers get toggle methods, but Pro unlocks precision control:

| Toggle | Free | Pro |
|:---|:---|:---|
| `toggleLoad(v)` | On/Off | Set specific state |
| `toggleHide(v)` | On/Off | Conditional with value |
| `toggleDrag(v)` | On/Off | Programmatic control |
| `toggleFloat(v)` | On/Off | Position management |

---

## Security in Pro

Pro builds include enterprise-grade security utilities:
- **AES-256 encryption/decryption** for sensitive config data
- **Encrypted JSON configs** — serve encrypted UI definitions, decrypted at runtime
- Premium utilities are **physically stripped** from free builds (not just hidden)

---

## How to Upgrade

```javascript
import Vue from 'vue';
import WBC from 'wbc-ui2';

Vue.use(WBC, {
  premiumKey: 'your-license-key'
});
```

Visit [wbc-ui.com](https://wbc-ui.com) for pricing and activation.

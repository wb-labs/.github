# WBC-UI2 — Architecture Overview

## How It Works

WBC-UI2 is a **runtime JSON-to-UI interpreter** for Vue.js. You give it a JSON object describing your UI, and it renders fully reactive Vue components.

```
JSON Config  -->  WBC Engine  -->  Reactive Vue Components
```

---

## The Core Concept

### The `<WBC>` Component

Everything starts with a single component:

```html
<WBC :item="myConfig" />
```

Where `myConfig` is any of:
- A string (rendered as text, markdown, or file path)
- An object (rendered as a Vue component)
- An array (rendered as a list of components)

### The Pipe Syntax

WBC-UI2 introduces a unique **pipe syntax** for declarative configuration:

```html
<WBC item="./config.json | pa-3 highlight-dark | https://example.com | python" />
```

This single string specifies:
1. **Source**: `./config.json` (the file to load)
2. **Styling**: `pa-3 highlight-dark` (CSS classes)
3. **Link**: `https://example.com` (wraps in a link)
4. **Parser**: `python` (force syntax highlighting language)

---

## Ecosystem Architecture

```
                    @wbc-ui2 Ecosystem
    ┌─────────────────────────────────────────────┐
    │                                             │
    │  ┌─────────────────────────────────────┐    │
    │  │         wbc-ui2 (Core Engine)       │    │
    │  │  JSON Parsing | Rendering | Tiering │    │
    │  └──────────────┬──────────────────────┘    │
    │                 │                           │
    │     ┌───────────┼───────────┐               │
    │     │           │           │               │
    │  ┌──┴──┐   ┌────┴───┐  ┌───┴────┐          │
    │  │Code │   │ Chart  │  │Mermaid │  ...      │
    │  │     │   │(ECharts)│  │        │          │
    │  └─────┘   └────────┘  └────────┘          │
    │                                             │
    └─────────────────────────────────────────────┘
```

Each package is:
- **Independent**: Install only what you need
- **Plugin-based**: Registers via `Vue.use()`
- **Tier-aware**: Respects Free/Pro licensing from the core store

---

## The `itemAccessebility` Proxy

Every WBC component exposes a controlled proxy object (called `that` in dive mode). This is the public API for interacting with rendered components.

**Why a proxy?** Instead of exposing the raw Vue instance (dangerous, unstable), WBC-UI2 provides a curated interface with tiered access:

```javascript
// Free tier: basic interaction
that.data        // Reactive state
that.emit('click', payload)
that.update()

// Pro tier: full orchestration
that.store       // Vuex store access
that.router      // Vue Router access
that.vm          // Raw Vue instance
that.watch('prop', callback)
```

---

## Lifecycle Hooks

WBC-UI2 supports logic injection via hooks:

```javascript
// In your JSON config or JS module:
{
  comp: 'v-card',
  init(that) {
    // Runs after mount — setup logic here
    that.data.title = 'Dynamic Title';
  },
  tracker(that) {
    // Runs on every render — reactive orchestration
  }
}
```

| Hook | Free | Pro | When It Runs |
|:---|:---:|:---:|:---|
| `init0` | Yes | Yes | Before mount (early setup) |
| `init` | Yes | Yes | After mount |
| `updater` | Yes | Yes | On each update |
| `setup` | - | Yes | Module-level setup |
| `tracker` | - | Yes | Per-render orchestration |
| `logic` | - | Yes | General logic injection |

---

## Build System

WBC-UI2 uses a three-tier build system:

| Build | Output | Purpose |
|:---|:---|:---|
| `dist-dev/` | All features + debugging | Local development |
| `dist-free/` | Premium code stripped | Public NPM distribution |
| `dist-pro/` | Full features | Licensed users |

Premium features are **physically removed** from free builds at compile time — not just hidden behind runtime checks.

---

## Getting Started

```bash
# Install
npm install wbc-ui2

# Optional packages
npm install @wbc-ui2/code    # Syntax highlighting
npm install @wbc-ui2/chart   # Data visualization
npm install @wbc-ui2/mermaid # Diagrams
npm install @wbc-ui2/latex   # Math formulas
```

```javascript
import Vue from 'vue';
import WBC from 'wbc-ui2';
import WBCode from '@wbc-ui2/code';

Vue.use(WBC);
Vue.use(WBCode);
```

- [Full Documentation](https://wbc-ui.com)
- [Live Demo](https://demo.wbc-ui.com)
- [npm](https://www.npmjs.com/package/wbc-ui2)

# @wbc-ui2 — The Low-Code Operating System for Vue

<p align="center">
  <img src="./logo/wbc-ui2.png" alt="WBC-UI2 Ecosystem" width="250"/>
</p>

<p align="center">
  <strong>Transform your Data into Interactive UIs. No boilerplate. No limits.</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/wbc-ui2"><img src="https://img.shields.io/npm/v/wbc-ui2?color=blue&amp;label=wbc-ui2" alt="npm wbc-ui2"/></a>
  <a href="https://www.npmjs.com/package/@wbc-ui2/code"><img src="https://img.shields.io/npm/v/@wbc-ui2/code?color=green&amp;label=@wbc-ui2/code" alt="npm code"/></a>
  <a href="https://www.npmjs.com/package/@wbc-ui2/chart"><img src="https://img.shields.io/npm/v/@wbc-ui2/chart?color=orange&amp;label=@wbc-ui2/chart" alt="npm chart"/></a>
  <a href="https://www.npmjs.com/package/@wbc-ui2/latex"><img src="https://img.shields.io/npm/v/@wbc-ui2/latex?color=red&amp;label=@wbc-ui2/latex" alt="npm latex"/></a>
  <a href="https://www.npmjs.com/package/@wbc-ui2/mermaid"><img src="https://img.shields.io/npm/v/@wbc-ui2/mermaid?color=purple&amp;label=@wbc-ui2/mermaid" alt="npm mermaid"/></a>
  <img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="License"/>
</p>

---

## 🏛️ The Vision

In a world of static component libraries, **@wbc-ui2** stands alone as a high-level **orchestration engine**. While others give you buttons, we give you a foundation to build intelligent, data-driven applications.

WBC-UI2 treats components as **Smart Entities** that handle their own context, rendering logic, and developer tools using simple JSON or JavaScript configurations.

### Core Tenets

- 📦 **UI as Data** — Define complex layouts in JSON. Move your UI logic to the backend or a CMS.
- ⚡ **Zero Plumbing** — Reactive state management, routing, and i18n are handled automatically by the engine.
- 🛡️ **Controlled Accessibility** — A secure proxy (`itemAccessebility`) ensures developers interact with a stable, safe API, not the raw Vue instance.
- 🌍 **Open Core** — A massive free engine for the community, supported by a "God Mode" (PRO) layer for enterprise power-users.

---

## ✨ Why WBC-UI2?

Most UI libraries give you components. **WBC-UI2 gives you an engine.**

### Render Any File as a Component

Point WBC at any file — Markdown, HTML, JSON, JavaScript, Python, LaTeX, Mermaid diagrams — and it renders intelligently:

```html
<WBC item="./readme.md" />
<WBC item="./chart-config.json" />
<WBC item="./diagram.mmd" />
<WBC item="./formula.tex" />
```

### The Pipe Syntax (PRO)

Combine content path, styling, link behavior, and parser override in a single string:

```html
<!-- Render a .txt file as Python with custom styling -->
<WBC item="./script.txt | pa-3 highlight-dark | | python" />

<!-- Render markdown with a link wrapper -->
<WBC item="./info.md | elevation-2 | https://wbc-ui.com" />
```

**Format:** `item="[FilePath] | [CSS_Classes] | [Link_URL] | [Explicit_Parser]"`

### Smart JavaScript Handling

WBC detects JS/TS files automatically: Vue components are rendered live, `@wbc-logic` files inject lifecycle hooks, plain objects become data-driven UIs, and everything else is displayed as a code snippet.

### Headless Content Extraction (PRO)

Go beyond rendering — programmatically access the generated HTML, Markdown, and VNodes:

```javascript
{
  output: {
    html: { pureHtml: "..." },
    md:   { pureMd: "..." },
    vNodes: { main: VNode, wbCode: VNode }
  }
}
```

---

## 📦 The Ecosystem

The `@wbc-ui2` project is a collection of modular packages designed to work in perfect harmony.

### Released Packages (v1.0.0)

| Package | Purpose | npm |
| :--- | :--- | :--- |
| `wbc-ui2` | **The Core Engine** — Orchestration, dynamic rendering, and logic injection. | [npm](https://www.npmjs.com/package/wbc-ui2) |
| `@wbc-ui2/code` | **Dev Experience** — Advanced syntax highlighting, code preview, and live editors. | [npm](https://www.npmjs.com/package/@wbc-ui2/code) |
| `@wbc-ui2/chart` | **Visualization** — Low-code wrapper for Chart.js and ECharts. | [npm](https://www.npmjs.com/package/@wbc-ui2/chart) |
| `@wbc-ui2/latex` | **Science** — High-fidelity TeX/LaTeX mathematical formula rendering. | [npm](https://www.npmjs.com/package/@wbc-ui2/latex) |
| `@wbc-ui2/mermaid` | **Diagrams** — Turn text descriptions into flowcharts and sequence diagrams. | [npm](https://www.npmjs.com/package/@wbc-ui2/mermaid) |

### Coming Soon

| Package | Planned Feature | Status |
| :--- | :--- | :--- |
| `@wbc-ui2/table` | **Data Tables** — Nested tables, JSON editing, and dynamic API form replacement. | 🟡 To Release |
| `@wbc-ui2/gis` | **GIS** — Intelligent Geographic Information System components (Leaflet). | 🟡 To Release |
| `@wbc-ui2/wbDataviewer` | **Data Insight** — Advanced JSON/JS object browsing with beautified depth and search. | 🟡 To Release |

---

## 🚀 Quick Start

### 1. Install

```bash
npm install wbc-ui2
```

### 2. Setup (Modern SPA — Vite / Webpack / Vue CLI)

In your main entry file (e.g., `main.js`):

```javascript
import Vue from 'vue';
import App from './App.vue';
import Vuetify from 'vuetify';
import 'vuetify/dist/vuetify.min.css';
import WBCUI2 from 'wbc-ui2';

// 1. Register framework plugins
Vue.use(Vuetify);

// 2. Install WBC-UI2 Core with context
Vue.use(WBCUI2, {
    context: require.context(".", true),  // Enables local file resolution
    // lg: 'ar'                           // Optional: force language (en, fr, ar)
});

// 3. Mount your app
new Vue({
    vuetify: new Vuetify(),
    render: (h) => h(App),
}).$mount('#app');
```

### 3. Adding Extension Packages

The WBC ecosystem is modular. Extensions register themselves into the core engine:

```javascript
import WBCode from '@wbc-ui2/code';
import WBChart from '@wbc-ui2/chart';
import WBMermaid from '@wbc-ui2/mermaid';
import WBLatex from '@wbc-ui2/latex';

Vue.use(WBCUI2);     // Core must be installed first
Vue.use(WBCode);     // Code editing and syntax highlighting
Vue.use(WBChart);    // ECharts data visualization
Vue.use(WBMermaid);  // Mermaid diagrams
Vue.use(WBLatex);    // LaTeX math rendering
```

> **Important**: Always install `wbc-ui2` (core) **before** any extensions. Extensions depend on the core's rendering pipeline.

### 4. Verify Installation

Add this to any Vue template to confirm WBC-UI2 is working:

```html
<WBC :item="{ comp: 'VAlert', options: { props: { type: 'success' }, html: 'WBC-UI2 is installed!' } }"></WBC>
```

### 5. CDN (No Build Step)

For quick prototyping without any build system:

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.7/dist/vue.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vuetify@2/dist/vuetify.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/wbc-ui2@latest/dist/wbc-ui2.umd.js"></script>
<script>
  Vue.use(Vuetify);
  Vue.use(WBCUI2);
  new Vue({
    vuetify: new Vuetify(),
    el: '#app',
  });
</script>
```

### Build Formats

| File | Format | Use Case |
| :--- | :--- | :--- |
| `wbc-ui2.es.js` | **ESM** | Modern bundlers (Vite, Webpack, Rollup) |
| `wbc-ui2.umd.js` | **UMD** | CDN / script tags in the browser |
| `wbc-ui2.full-embed.es.js` | **Full-Embed ESM** | Standalone apps — CSS is injected by JS |
| `wbc-ui2.full-embed.umd.js` | **Full-Embed UMD** | Standalone browser apps — no separate CSS needed |

> **Tip**: The **Full-Embed** variants bundle the CSS directly into the JS. No separate `.css` import is needed.

### Vite Plugin

WBC-UI2 includes a dedicated Vite plugin for optimal developer experience:

```javascript
// vite.config.js
import { wbcVitePlugin } from 'wbc-ui2/vite-plugin';

export default {
  plugins: [...wbcVitePlugin()]
};
```

### Webpack Plugin

For Webpack-based projects:

```javascript
// vue.config.js
module.exports = {
  chainWebpack: (config) => {
    require('wbc-ui2/wbc.webpack.js').chainWebpack(config);
  }
};
```

---

## 🏗️ Architecture — `itemAccessebility`

The user **never** sees the raw Vue instance. Instead, they interact through a **controlled proxy** called `itemAccessebility`:

```
┌───────────────────────────────────────────────────┐
│  User's World (item config with dive=true)        │
│                                                   │
│  comp: (that) => ...       // dynamic component   │
│  class: (that) => ...      // dynamic styling     │
│  click: (that, evt) => ... // interactive events   │
│  init: (that) => ...       // lifecycle setup      │
│                                                   │
│  "that" = itemAccessebility (the ONLY interface)  │
└───────────┬───────────────────────────────────────┘
            │  ← This is the GATE
┌───────────▼───────────────────────────────────────┐
│  WBC Internal World (Vue instance)                │
│  itemAccessebility decides what leaks through.    │
└───────────────────────────────────────────────────┘
```

When `dive=true`, every property of the WBC item can be written as a function of `that`. Everything becomes dynamic:

```javascript
{
  dive: true,
  comp: (that) => that.lg.lang == 'en' ? 'VBtn' : 'VCard',
  options: {
    class: (that) => that.data.comp == 'VBtn' ? 'red' : 'green',
    on: {
      click: (that, evt) => that.toggleHide(true)
    }
  }
}
```

---

## 💎 Free vs Pro

### Component Interface (`itemAccessebility`)

| Property / Method | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| **Identity and Data** | | | |
| `userTier` | ✅ | ✅ | Returns 'Free', 'Premium', or 'Development'. |
| `nameEl` | ✅ | ✅ | The global identifier or resolved component name. |
| `props` | ✅ | ✅ | The raw Vue props of the WBC instance. |
| `data` | ✅ | ✅ | Reactive bridge to the component's internal state. |
| `license` | ❌ | ✅ | The validated license object from store. |
| `data0` | ❌ | ✅ | Access to the original, non-reactive component definition. |
| `vm` | ❌ | ✅ | Raw Vue Instance for deep architectural access. |
| **State Management** | | | |
| `update(v)` | ✅ | ✅ | Forces a component update cycle. |
| `emit(ev, val)` | ✅ | ✅ | Emits Vue events. |
| `get(key)` | ❌ | ✅ | Explicitly get a data property. |
| `set(val, key)` | ❌ | ✅ | Explicitly set a data property. |
| `val(v)` | ❌ | ✅ | High-level value getter/setter with validation. |
| **Framework Access** | | | |
| `store` | ❌ | ✅ | Access to Vuex store instance. |
| `router` | ❌ | ✅ | Access to Vue Router instance. |
| `routes` | ❌ | ✅ | Dictionary of all registered routes. |
| `routeParams` | ❌ | ✅ | Current URL parameters. |
| `ref(name)` | ❌ | ✅ | Access to child components via `$refs`. |
| `el` | ❌ | ✅ | Access to the raw DOM element. |
| `root` | ❌ | ✅ | The root Vue instance. |
| `watch(p, cb)` | ❌ | ✅ | Dynamic property watcher. |
| **Logic and Services** | | | |
| `dayjs` | ⚠️ Limited | ✅ Full | Date manipulation utility. |
| `storage` | ⚠️ Basic | ✅ Full | LocalStorage bridge. |
| `cookies` | ⚠️ Basic | ✅ Full | Browser cookies bridge. |
| `markdown` | ❌ | ✅ | Bi-directional MD/HTML transformation. |
| `aes` (Enc/Dec) | ❌ | ✅ | Enterprise AES-256 encryption utilities. |
| `queryData` | ❌ | ✅ | High-level API fetcher with cache logic. |
| `trigger(method)` | ❌ | ✅ | Execute any public component method by name. |

### Logic Injection Hooks

| Hook | Free | Pro | Description |
| :--- | :---: | :---: | :--- |
| `init(ctx)` | ✅ | ✅ | Early initialization. Runs for all tiers. |
| `setup(ctx)` | ❌ | ✅ | Module-level setup. |
| `tracker(ctx)` | ❌ | ✅ | Per-render orchestration. |
| `logic(ctx)` | ❌ | ✅ | General module logic injection. |
| `@wbc-logic` (Func) | ❌ | ✅ | Pure function injection. |
| `output` (Prop) | ❌ | ✅ | **God Mode Layout**: Transform resolve into actual VNodes. |

---

## 🌐 Live Demos and Documentation

### @wbc-ui2/core

| Resource | URL |
| :--- | :--- |
| **Official Site and Docs** | [wbc-ui.com](https://wbc-ui.com) |
| **Live Demo App** | [demo.wbc-ui.com](https://www.demo.wbc-ui.com) |
| **Markdown Demo** | [md.wbc-ui.com](https://md.wbc-ui.com) |
| **Routing Demo** | [wbRoutes2.wbc-ui2.com](https://wbRoutes2.wbc-ui2.com) |
| **WB-Press Docs** | [wb-press.wbc-ui2.com](https://wb-press.wbc-ui2.com) |
| **Starter Template (Vite)** | *Coming soon* |
| **Starter Template (Webpack)** | *Coming soon* |
| **Starter Template (Vue CLI)** | *Coming soon* |

### @wbc-ui2/code

| Resource | URL |
| :--- | :--- |
| **Documentation** | [wbcode2.wbc-ui.com](https://wbcode2.wbc-ui.com) |
| **Live Demo** | [wbcode2.wbc-ui.com/demo](https://wbcode2.wbc-ui.com) |
| **Starter Template (Vite)** | *Coming soon* |
| **Starter Template (Webpack)** | *Coming soon* |
| **Starter Template (Vue CLI)** | *Coming soon* |

### @wbc-ui2/chart

| Resource | URL |
| :--- | :--- |
| **Documentation** | [wb-chart.wbc-ui.com](https://wb-chart.wbc-ui.com) |
| **Live Demo** | [wb-chart.wbc-ui.com/demo](https://wb-chart.wbc-ui.com) |
| **Starter Template (Vite)** | *Coming soon* |
| **Starter Template (Webpack)** | *Coming soon* |
| **Starter Template (Vue CLI)** | *Coming soon* |

### @wbc-ui2/mermaid

| Resource | URL |
| :--- | :--- |
| **Documentation** | [wb-mermaid.wbc-ui.com](https://wb-mermaid.wbc-ui.com) |
| **Live Demo** | [wb-mermaid.wbc-ui.com/demo](https://wb-mermaid.wbc-ui.com) |
| **Starter Template (Vite)** | *Coming soon* |
| **Starter Template (Webpack)** | *Coming soon* |
| **Starter Template (Vue CLI)** | *Coming soon* |

### @wbc-ui2/latex

| Resource | URL |
| :--- | :--- |
| **Documentation** | *Coming soon* |
| **Live Demo** | *Coming soon* |
| **Starter Template (Vite)** | *Coming soon* |
| **Starter Template (Webpack)** | *Coming soon* |
| **Starter Template (Vue CLI)** | *Coming soon* |

---

## 🌐 Roadmap 2026

- ✅ **Q1 2026** — Stable Core release + Pro licensing engine.
- 🚧 **Q2 2026** — Launch of the "Interactive Lab" at wbc-ui.com.
- 🔮 **Q3 2026** — The Vue 3 and TypeScript Revolution (Native rewrite).
- 🔮 **2027** — Visual Builder — A drag-and-drop interface for generating WBC data.

---

## 📣 Community and Social

| Platform | Link |
| :--- | :--- |
| **Dev.to** | [dev.to/wbc-ui](https://dev.to/wbc-ui) |
| **Twitter / X** | @wbc_ui |
| **LinkedIn** | [WBC-UI Official](https://linkedin.com/company/wbc-ui) |

---

## 👨‍💻 About the Author

**Wissem Boughamoura**
*Senior Software Architect and Full-Stack Systems Engineer*

The `@wbc-ui2` project is the culmination of years of experience in high-security, high-performance enterprise application development. Wissem specializes in creating abstract architectural layers that bridge the gap between complex backend data and reactive frontend interfaces.

- 🌐 **Portfolio**: [wi-bg.com](https://www.wi-bg.com)
- 🐙 **GitHub**: [@wissemb11](https://github.com/wissemb11)
- 💼 **LinkedIn**: [Wissem Boughamoura](https://linkedin.com/in/wissemb11)
- 📧 **Contact**: [wissemb11@gmail.com](mailto:wissemb11@gmail.com)

---

## 📄 License

This project is governed by an **Open Core** model. The core engine is released under the **MIT License**. For "God Mode" (PRO) features and enterprise support, please see the licensing terms at [wbc-ui.com](https://wbc-ui.com).

Copyright © 2026 Wissem Boughamoura.

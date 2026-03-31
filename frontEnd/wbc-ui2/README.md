# WBC-UI — The Low-Code Operating System for Vue

<p align="center">
  <img src="https://wbc-ui.com/logo.png" alt="WBC-UI" width="200"/>
</p>

<p align="center">
  <strong>Transform your Data into Interactive UIs. No boilerplate. No limits.</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/wbc-ui2"><img src="https://img.shields.io/npm/v/wbc-ui2?color=blue&label=wbc-ui2" alt="npm wbc-ui2"/></a>
  <a href="https://wbc-ui.com"><img src="https://img.shields.io/badge/docs-wbc--ui.com-blue?style=flat-square" alt="Docs"/></a>
  <img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="License"/>
</p>

---

## Overview

**WBC-UI** is a product line within [WB-Labs](../../README.md) focused on building the most powerful low-code component ecosystem for Vue.js.

Instead of assembling individual components, WBC-UI provides an **orchestration engine** that turns raw data — JSON, Markdown, JavaScript, LaTeX, Mermaid diagrams, and more — into fully interactive, production-ready interfaces.

---

## Product Versions

### [`core2/`](core2/README.md) — Stable Release (Vue 2) ✅

The current production-ready monorepo built on **Vue 2.7 + Vuetify 2**. This is the actively published and deployed version.

- **Version**: `1.0.0`
- **Status**: Stable, published on npm
- **Packages**: 5 released (`wbc-ui2`, `@wbc-ui2/code`, `@wbc-ui2/chart`, `@wbc-ui2/latex`, `@wbc-ui2/mermaid`)
- **Apps**: 20+ demo sites, doc portals, and starter templates
- **Build System**: Vite 6 with custom Vite plugin

➡️ **[Full Documentation & Setup →](core2/README.md)**

### `core3/` — Next Generation (Vue 3) 🔮

The planned native rewrite targeting **Vue 3 + TypeScript** with Composition API. Expected in Q3 2026.

- **Status**: Planned
- **Goals**: First-class TypeScript, Composition API, tree-shakeable ESM, modern SSR support

---

## Ecosystem at a Glance

| Package | Purpose | npm |
| :--- | :--- | :--- |
| `wbc-ui2` | **Core Engine** — Orchestration, dynamic rendering, logic injection | [npm](https://www.npmjs.com/package/wbc-ui2) |
| `@wbc-ui2/code` | **Code** — Syntax highlighting, live editors, code preview | [npm](https://www.npmjs.com/package/@wbc-ui2/code) |
| `@wbc-ui2/chart` | **Charts** — Low-code Chart.js and ECharts wrapper | [npm](https://www.npmjs.com/package/@wbc-ui2/chart) |
| `@wbc-ui2/latex` | **LaTeX** — High-fidelity mathematical formula rendering | [npm](https://www.npmjs.com/package/@wbc-ui2/latex) |
| `@wbc-ui2/mermaid` | **Diagrams** — Text-to-flowchart/sequence diagram | [npm](https://www.npmjs.com/package/@wbc-ui2/mermaid) |

### Coming Soon

| Package | Description |
| :--- | :--- |
| `@wbc-ui2/table` | Nested tables, JSON editing, dynamic API forms |
| `@wbc-ui2/gis` | Geographic Information System (Leaflet) |
| `@wbc-ui2/wbDataviewer` | JSON/JS object browser with depth search |

---

## Live Demos

| Resource | URL |
| :--- | :--- |
| Official Site & Docs | [wbc-ui.com](https://wbc-ui.com) |
| Core Demo | [demo.wbc-ui.com](https://www.demo.wbc-ui.com) |
| Code Editor Demo | [wbcode2.wbc-ui.com](https://wbcode2.wbc-ui.com) |
| Chart Demo | [wb-chart.wbc-ui.com](https://wb-chart.wbc-ui.com) |
| Mermaid Demo | [wb-mermaid.wbc-ui.com](https://wb-mermaid.wbc-ui.com) |
| Markdown Demo | [md.wbc-ui.com](https://md.wbc-ui.com) |
| Routing Demo | [wbRoutes2.wbc-ui2.com](https://wbRoutes2.wbc-ui2.com) |
| WB-Press Docs | [wb-press.wbc-ui2.com](https://wb-press.wbc-ui2.com) |

---

## Quick Start

```bash
npm install wbc-ui2
```

```javascript
import Vue from 'vue';
import Vuetify from 'vuetify';
import WBCUI2 from 'wbc-ui2';

Vue.use(Vuetify);
Vue.use(WBCUI2, { context: require.context(".", true) });

new Vue({
  vuetify: new Vuetify(),
  render: (h) => h(App),
}).$mount('#app');
```

➡️ **[Full setup guide, architecture docs, and Pro features →](core2/README.md)**

---

## License

Open Core model — the core engine is **MIT**. Pro features are available under separate terms. See [core2/README.md](core2/README.md) for details.

Copyright © 2026 Wissem Boughamoura.

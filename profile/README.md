# WB-Labs

<p align="center">
  <img src="https://wbc-ui.com/logo.png" alt="WB-Labs" width="200"/>
</p>

<p align="center">
  <strong>Engineering the Future of Developer Infrastructure</strong><br/>
  <em>A product-driven R&D lab building tools that make software development smarter, faster, and more accessible.</em>
</p>

<p align="center">
  <a href="https://wbc-ui.com"><img src="https://img.shields.io/badge/web-wbc--ui.com-blue?style=flat-square" alt="Website"/></a>
  <a href="https://www.npmjs.com/package/wbc-ui2"><img src="https://img.shields.io/npm/v/wbc-ui2?color=blue&label=wbc-ui2&style=flat-square" alt="npm"/></a>
  <a href="https://github.com/wissemb11"><img src="https://img.shields.io/badge/GitHub-wissemb11-181717?style=flat-square&logo=github" alt="GitHub"/></a>
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" alt="Status"/>
</p>

---

## 🧬 What is WB-Labs?

**WB-Labs** is the umbrella organization for the software products, libraries, and tools created by **Wissem Boughamoura**. Our mission: **build less, deliver more.**

We design high-level orchestration engines and developer tools that eliminate boilerplate and transform raw data into production-ready interfaces.

---

## 🏹 Flagship Product: @wbc-ui2

**WBC-UI2** is a low-code, component orchestration ecosystem for Vue.js. It transforms raw data — JSON, Markdown, JavaScript, LaTeX, Mermaid diagrams — into fully interactive UIs with zero boilerplate.

```html
<WBC item="./readme.md" />
<WBC item="./chart-config.json" />
<WBC item="./diagram.mmd" />
<WBC item="./formula.tex" />
```

### Published Packages (v1.0.0)

| Package | Description | npm |
| :--- | :--- | :--- |
| **`wbc-ui2`** | The Core Engine — Dynamic rendering and orchestration | [![npm](https://img.shields.io/npm/v/wbc-ui2?color=blue&style=flat-square)](https://www.npmjs.com/package/wbc-ui2) |
| **`@wbc-ui2/code`** | Advanced syntax highlighting and live editors | [![npm](https://img.shields.io/npm/v/@wbc-ui2/code?color=green&style=flat-square)](https://www.npmjs.com/package/@wbc-ui2/code) |
| **`@wbc-ui2/chart`** | Low-code Chart.js and ECharts wrapper | [![npm](https://img.shields.io/npm/v/@wbc-ui2/chart?color=orange&style=flat-square)](https://www.npmjs.com/package/@wbc-ui2/chart) |
| **`@wbc-ui2/latex`** | TeX/LaTeX mathematical formula rendering | [![npm](https://img.shields.io/npm/v/@wbc-ui2/latex?color=red&style=flat-square)](https://www.npmjs.com/package/@wbc-ui2/latex) |
| **`@wbc-ui2/mermaid`** | Text-to-diagram rendering (flowcharts, sequences) | [![npm](https://img.shields.io/npm/v/@wbc-ui2/mermaid?color=purple&style=flat-square)](https://www.npmjs.com/package/@wbc-ui2/mermaid) |

### Quick Start

```bash
npm install wbc-ui2
```

```javascript
import Vue from 'vue';
import Vuetify from 'vuetify';
import WBCUI2 from 'wbc-ui2';

Vue.use(Vuetify);
Vue.use(WBCUI2, { context: require.context(".", true) });
```

➡️ **Full docs, architecture, and API reference: [see Documentation →](../docs/wbc-ui2/)**

---

## 💎 The Open Core Model

WBC-UI2 follows the **Open Core** model — a massive free engine for the community, supported by a Pro layer for power-users.

| | 🟢 Free (Base) | 🔴 Pro (Premium) |
| :--- | :--- | :--- |
| **Rendering** | Strings, Objects, Files, Lists | + Encrypted Configs, Remote Logic |
| **Lifecycle** | 3 hooks (`init0`, `init`, `updater`) | + 4 architect hooks (`tracker`, `logic`, `setup`, `watch`) |
| **API (`that`)** | State toggles, `data`, i18n, auth | + `vm`, `store`, `router`, `data0`, `content` extraction |
| **Services** | Basic `dayjs`, `storage`, `cookies` | + Full access, `aes` encryption, `markdown`, `queryData` |
| **Philosophy** | *"Build with it"* | *"Command it"* |

> **"Free users can bind states. Pro users can command them."**
> **"3 hooks for builders, 7 hooks for architects."**

➡️ **[Full Free vs Pro comparison →](../docs/wbc-ui2/strategy/free-vs-pro.md)**

---

## 🌐 Live Demos

| Demo | URL |
| :--- | :--- |
| 🏠 Official Site & Docs | [wbc-ui.com](https://wbc-ui.com) |
| 🚀 Core Demo | [demo.wbc-ui.com](https://www.demo.wbc-ui.com) |
| 💻 Code Editor | [wbcode2.wbc-ui.com](https://wbcode2.wbc-ui.com) |
| 📊 Charts | [wb-chart.wbc-ui.com](https://wb-chart.wbc-ui.com) |
| 📐 Mermaid Diagrams | [wb-mermaid.wbc-ui.com](https://wb-mermaid.wbc-ui.com) |
| 📝 Markdown Renderer | [md.wbc-ui.com](https://md.wbc-ui.com) |
| 🔀 Routing Demo | [wbRoutes2.wbc-ui2.com](https://wbRoutes2.wbc-ui2.com) |
| 📖 WB-Press Docs | [wb-press.wbc-ui2.com](https://wb-press.wbc-ui2.com) |

---

## 🗓️ Roadmap

| Timeline | Milestone |
| :--- | :--- |
| ✅ Q1 2026 | WBC-UI2 Core v1.0.0 — Stable release with Pro licensing engine |
| 🚧 Q2 2026 | Interactive Lab + Table, GIS, DataViewer packages |
| 🔮 Q3 2026 | Vue 3 + TypeScript native rewrite |
| 🔮 2027 | Visual Builder — drag-and-drop UI generation |

---

## 🗂️ Organization Structure

```
wb-labs/
├── frontEnd/                   ← Frontend products
│   └── wbc-ui/                 ← WBC-UI product line
│       ├── core2/              ← Stable Vue 2 monorepo (v1.0.0) ✅
│       └── core3/              ← Vue 3 + TypeScript (planned)
├── backEnd/                    ← Backend services (Django — planned)
├── mobile/                     ← Mobile apps (planned)
├── chromeExtension/            ← Browser extensions (planned)
└── VSExtension/                ← VS Code extensions (planned)
```

---

## 📚 Public Documentation

Detailed public documentation for the WBC-UI2 ecosystem is available in this repository:

| Document | Description |
| :--- | :--- |
| [Architecture & Flow](../docs/wbc-ui2/architecture/technical-architecture.md) | How the engine works: bootstrapping, rendering, tiering |
| [File Handling Guide](../docs/wbc-ui2/architecture/file-handling.md) | Smart file detection, JS case analysis, Pipe syntax |
| [Free vs Pro](../docs/wbc-ui2/strategy/free-vs-pro.md) | Complete feature comparison table |
| [Roadmap 2026](../docs/wbc-ui2/strategy/roadmap-2026.md) | Strategic milestones and monetization plan |
| [Vue 3 Vision](../docs/wbc-ui2/strategy/vue3-vision.md) | TypeScript migration blueprint |
| [wbc-ui2 (Core)](../docs/wbc-ui2/packages/wbc-ui2.md) | Core engine README |
| [@wbc-ui2/code](../docs/wbc-ui2/packages/wbc-ui2-code.md) | Code package README |
| [Apps Directory](../docs/wbc-ui2/apps/apps-directory.md) | All demos, doc portals, and starter templates |
| [Ecosystem Hub](../docs/wbc-ui2/ecosystem-resources.md) | npm links, URLs, community |

---

## 🧑‍💻 About the Author

**Wissem Boughamoura** — *Senior Software Architect & Full-Stack Systems Engineer*

| | |
| :--- | :--- |
| 🌐 Portfolio | [wi-bg.com](https://www.wi-bg.com) |
| 🐙 GitHub | [@wissemb11](https://github.com/wissemb11) |
| 💼 LinkedIn | [Wissem Boughamoura](https://linkedin.com/in/wissemb11) |
| 📧 Contact | [wissemb11@gmail.com](mailto:wissemb11@gmail.com) |

---

## 📄 License

The core engine is released under the **MIT License**. Pro features are available under separate licensing terms — see package documentation for details.

Copyright © 2026 Wissem Boughamoura.

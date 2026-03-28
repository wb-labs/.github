# wbc-ui2 — The Core Engine

**wbc-ui2** is a versatile Vue.js plugin offering a collection of reusable UI components and utilities for modern web applications. Built with Vue 2 and seamlessly integrated with Vuetify, it provides a polished, Material Design-based user interface.

## Features

- **Smart Rendering Engine** — Point WBC at any file (Markdown, JSON, JS, LaTeX, Mermaid) and it renders intelligently.
- **Advanced File Orchestration** — Use the Pipe (`|`) syntax for styling, linking, and parser overrides (PRO).
- **Headless Content Extraction** — Access clean HTML, Markdown, and VNodes programmatically (PRO).
- **Vuetify Integration** — Leverages Vuetify for consistent Material Design styling.
- **Multiple Build Formats** — ESM, UMD, and Full-Embed variants.

## Architecture — `itemAccessebility` as the ONLY Interface

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

## Free vs Pro

| Feature | Free | Pro |
| :--- | :---: | :---: |
| Smart Rendering Engine | ✅ | ✅ |
| State Toggles (hide, float, drag, close) | ✅ | ✅ |
| i18n, Form Support, Auth-Aware | ✅ | ✅ |
| Basic Lifecycle (`init0`, `init`, `updater`) | ✅ | ✅ |
| God Mode API (`vm`, `refs`, `data0`, `trigger`) | ❌ | ✅ |
| Content Extraction Pipeline | ❌ | ✅ |
| Advanced Lifecycle (`tracker`, `watch`, `logic`, `setup`) | ❌ | ✅ |
| Store, Router, Cookies, Storage Access | ❌ | ✅ |

## Installation

```bash
npm install wbc-ui2
```

## Usage (ESM)

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

## CDN (No Build Step)

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.7/dist/vue.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vuetify@2/dist/vuetify.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/wbc-ui2@latest/dist/wbc-ui2.umd.js"></script>
<script>
  Vue.use(Vuetify);
  Vue.use(WBCUI2);
  new Vue({ vuetify: new Vuetify(), el: '#app' });
</script>
```

## Build Formats

| File | Format | Use Case |
| :--- | :--- | :--- |
| `wbc-ui2.es.js` | **ESM** | Modern bundlers (Vite, Webpack, Rollup) |
| `wbc-ui2.umd.js` | **UMD** | CDN / script tags |
| `wbc-ui2.full-embed.es.js` | **Full-Embed ESM** | Standalone — CSS injected by JS |
| `wbc-ui2.full-embed.umd.js` | **Full-Embed UMD** | Standalone browser — no separate CSS |

## Dependencies

- **Required**: `vue` (^2.7.0), `vuetify` (^2.7.0), `vuex` (^3.6.0), `vue-router` (^3.5.0)
- **Optional**: `highlight.js`, `leaflet`, `prettier`, `pdfjs-dist`

## License

MIT — See [wbc-ui.com](https://wbc-ui.com) for Pro licensing terms.

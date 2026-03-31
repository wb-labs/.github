# wbc-ui2

<p align="center">
  <img src="../logo/wb-core.png" alt="WB-Core Logo" width="180"/>
</p>

<p align="center">
  <strong>Dynamic, Data-Driven UI Orchestration for Vue 2.7+</strong><br/>
  Define components as JSON. Control them with an Engine. Unlock "God Mode."
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/wbc-ui2"><img src="https://img.shields.io/npm/v/wbc-ui2.svg" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/wbc-ui2"><img src="https://img.shields.io/npm/dm/wbc-ui2.svg" alt="npm downloads"></a>
  <a href="https://github.com/wissemb11/wbc-ui2/blob/main/LICENSE"><img src="https://img.shields.io/npm/l/wbc-ui2.svg" alt="license"></a>
</p>

---

## 🚀 The Concept: "UI Components as Data"

**WBC-UI2** is a versatile Vue.js plugin that transforms how you build user interfaces. Instead of writing thousands of lines of boilerplate HTML templates, you define your UI programmatically using JSON configurations. 

The **`<WBC>`** component acts as a high-level **rendering engine**, turning simple data structures into fully functional, reactive components with built-in state, routing, and developer tools.

### **Traditional vs. WBC-UI2**
```javascript
// Before: 50+ lines of <template> for a dynamic card
// After: One smart component
<WBC :item="{
  comp: 'v-card',
  options: {
    props: { elevation: 3 },
    html: '<h4>Hello, World!</h4>',
    class: 'pa-4 blue white--text'
  }
}" />
```

---

## ✨ Features at a Glance
- 🎨 **Low-Code UI** - Define layouts with JSON/JS objects.
- ⚡ **Framework Fusion** - Vuetify (Material) + Bootstrap integration.
- 🧪 **Interactive Testing** - Built-in debugging indicators and source views.
- 🛡️ **Secure Access Gate** - Stable `itemAccessebility` proxy for all operations.
- 🌍 **Internationalization** - Built-in reactive i18n support.
- 📦 **Build Variations** - 7 variants from `base` (1.4MB) to `full-embed` (18MB).
- 🔌 **monorepo Ready** - Part of an ecosystem with `@wbc-ui2/code`, `chart`, `mermaid`, and `latex`.

---

## 🔌 Quick Start & Integration

### 1. Installation
```bash
npm install wbc-ui2
```

### 2. Main Entry (`main.js`)
WBC-UI2 requires a Vuetify instance to be provided to its plugin system.

```javascript
import Vue from 'vue';
import Vuetify from 'vuetify';
import wbcUi2 from 'wbc-ui2';
import 'wbc-ui2/dist/style.css'; // Not required for full-embed

const vuetifyInst = new Vuetify();

Vue.use(wbcUi2, {
  plugins: [
    { 
        name: 'Vuetify', 
        property: '$vuetify', 
        fallback: Vuetify, 
        fallbackInstance: vuetifyInst 
    }
  ]
});

new Vue({
  vuetify: vuetifyInst,
  render: h => h(App)
}).$mount('#app');
```

---

## ⚡ Mastering the Engine: `itemAccessebility` (ctx)

WBC-UI2 enforces a clean architecture. You never interact with the raw Vue instance. Instead, you use the **`itemAccessebility`** (ctx) proxy.

### **The Magic of `dive: true`**
When `dive: true` is set, every property becomes a function of the system state:

```javascript
{
  dive: true,
  comp: (ctx) => ctx.lg.lang == 'en' ? 'VBtn' : 'VCard',
  options: {
    class: (ctx) => ctx.data.comp == 'VBtn' ? 'red' : 'green',
    on: {
      click: (ctx, evt) => ctx.toggleHide(true) // High-level API
    }
  }
}
```

---

## 💎 Unlock "God Mode" (PRO Features)

WBC-UI2 is free to use for basic rendering. However, for elite architects, the **Pro License** unlocks a different class of development.

| Feature Group | Base (Free) | Pro | Description |
| :--- | :---: | :---: | :--- |
| **Logic Hooks** | `init` | `setup`, `tracker`, `logic` | Advanced lifecycle orchestration. |
| **Reactive Hub** | `data` | `data0`, `vm`, `refs`, `trigger` | **"God Mode"**: Control every part of the app. |
| **Pipes (|)** | ✅ (Basic) | ✅ (Full) | Force parse any file (e.g., `.txt` as `.js`). |
| **Extraction** | ❌ | ✅ | **Headless**: Access clean HTML, MD, and VNodes programmatically. |
| **Infrastructure** | ❌ | ✅ | Direct access to `store`, `router`, and `storage`. |
| **Layout** | ❌ | ✅ | **`output` property**: Structural transformation of sub-vNodes. |

👉 **[Upgrade to Pro at wbc-ui.com](https://wbc-ui.com)**

---

## 📂 Handling Files (Vite / Webpack)

WBC-UI2 ships with a dedicated Vite plugin to resolve local files:

```javascript
// vite.config.js
import { wbcVitePlugin } from 'wbc-ui2/vite-plugin';

export default {
    plugins: [
        ...wbcVitePlugin(), // Scans your source for local file imports
    ],
};
```

---

## 🧔 Author
**Wissem Boughamoura**
*Full-Stack Solutions Architect*

The vision for WBC-UI2 is to bridge the gap between complex enterprise data and reactive frontends by treating UI as an interpretable data structure.

- **🌐 Portfolio**: [wi-bg.com](https://www.wi-bg.com)
- **🐙 GitHub**: [@wissemb11](https://github.com/wissemb11)
- **📧 Contact**: [wissemb11@gmail.com](mailto:wissemb11@gmail.com)

---

## 📄 License
The core engine is licensed under the **MIT License**.
Copyright © 2026 Wissem Boughamoura.

# Why wb-core? The Engine Behind WBC-UI

> **wb-core** is not another component library. It is a content orchestration engine for Vue that turns any data -- strings, objects, files, URLs, Markdown, PDFs -- into a fully rendered, interactive UI through a single component.

---

## The Problem

Modern web development is mostly plumbing. You install a Markdown parser. A PDF viewer. A code highlighter. A chart library. A file handler. Then you write `v-if` chains to decide which one to use. You wire up reactivity, manage state, handle edge cases, and repeat for every project.

**80% of your time goes to infrastructure. 20% goes to your actual product.**

wb-core inverts that ratio.

## The Solution: One Component, Any Content

At the heart of the WBC-UI ecosystem is the `<WBC>` component. It accepts a single `item` prop and intelligently resolves how to render it:

```html
<!-- A string becomes text -->
<WBC item="Hello, world" />

<!-- A URL becomes a rendered page -->
<WBC item="https://example.com/data.json" />

<!-- A file path becomes a viewer -->
<WBC item="./report.pdf" />

<!-- A Markdown file becomes formatted content -->
<WBC item="./docs/guide.md" />

<!-- An object becomes a dynamic component tree -->
<WBC :item="{ comp: 'VCard', title: 'Dashboard', children: [...] }" />
```

No `v-if` chains. No manual parser imports. One component handles strings, arrays, objects, files (JS, TS, Markdown, JSON, PDF, images, video, audio), remote URLs, and nested component trees.

## The Architecture: `itemAccessebility` as the Only Interface

Users never touch the raw Vue instance. Instead, every WBC component exposes a controlled proxy called `itemAccessebility` (aliased as `that` in dive mode). This proxy is the gate between your application logic and the WBC engine:

```javascript
{
  dive: true,
  comp: (that) => that.lg.lang === 'en' ? 'VBtn' : 'VCard',
  options: {
    class: (that) => that.data.comp === 'VBtn' ? 'red' : 'green',
    on: {
      click: (that) => that.toggleHide(true)
    }
  }
}
```

When `dive=true`, every property becomes a **function of the system state**. Components, styles, event handlers, and lifecycle hooks all react dynamically. The developer describes *what* should happen; wb-core handles *how*.

## What You Get for Free

Every developer who installs wb-core gets a production-ready toolkit:

- **Smart rendering engine** -- strings, arrays, objects, and file rendering out of the box
- **State toggles** -- `toggleHide`, `toggleFloat`, `toggleDrag`, `toggleClose`, `toggleLoad`, `toggleProtected`
- **Reactive data bridge** -- `data`, `protected`, `load`, `float`, `drag`, `close`, `hide`
- **Form support** -- `val { set, get }`, `isValid`, `isValidFn`
- **Internationalization** -- `lg { lang, get, set }`
- **Auth-aware rendering** -- `user`, `loggedIn`
- **Three lifecycle hooks** -- `init0`, `init`, `updater`
- **Utilities** -- `ref`, `el`, `update`, `alert`, `dayjs`

## What Pro Unlocks

For teams building serious applications, the Pro tier unlocks a different class of development:

- **God Mode API** -- Direct access to `vm`, `data0`, `refs`, `emit`, `trigger` for full component control
- **Content extraction** -- Programmatic access to clean HTML, Markdown, and VNodes for headless use, SEO, and testing
- **Advanced lifecycle** -- Seven hooks (`tracker`, `watch`, `logic`, `setup` + the free three) for architects who need per-render orchestration
- **Infrastructure access** -- `store`, `router`, `routes`, `watch` for cross-component synchronization
- **Data tools** -- `set/get` (arbitrary key access), `markdown` (bi-directional MD/HTML), `aes` (encryption), `lzStr`, `cookies`, `storage`
- **Dynamic layout orchestration** -- The `output` property lets you remap internal VNodes into entirely custom layouts

> "Free users can bind states. Pro users can command them."
> "3 hooks for builders. 7 hooks for architects."

## Why Not Just Use Vuetify / PrimeVue / Quasar?

wb-core does not compete with UI frameworks -- it **augments** them. Vuetify gives you buttons, cards, and dialogs. wb-core gives you an engine that can dynamically compose those buttons, cards, and dialogs from a JSON configuration, a remote file, or a logic provider.

You use Vuetify for design. You use wb-core for orchestration.

## Built for the Real World

- **Multiple build variants**: Standard (175 KB gzipped: 49 KB), With-Prettier (~1.4 MB), Full-Embed (~7.8 MB for CDN/demos)
- **Multiple module formats**: ESM for bundlers, UMD for browsers
- **Three starter templates**: Vite, Vue CLI, and Webpack
- **Enterprise licensing**: Zero-latency validation, 24-hour cache, fail-open security (legitimate users are never blocked)

## Quick Install

```bash
npm install wbc-ui2 vue vuetify vuex vue-router
```

```javascript
import Vue from 'vue';
import Vuetify from 'vuetify';
import WbcUi2Plugin from 'wbc-ui2';
import 'wbc-ui2/dist/style.css';

const vuetifyInst = new Vuetify();

Vue.use(WbcUi2Plugin, {
  plugins: [
    { name: 'Vuetify', property: '$vuetify', fallback: Vuetify, fallbackInstance: vuetifyInst }
  ]
});

new Vue({
  vuetify: vuetifyInst,
  render: (h) => h(App)
}).$mount('#app');
```

Then use it anywhere:

```html
<WBC item="./welcome.md" />
<WBC :item="dashboardConfig" />
<WBC item="https://api.example.com/content.json" />
```

## Links

- **npm**: [npmjs.com/package/wbc-ui2](https://www.npmjs.com/package/wbc-ui2)
- **Documentation**: [wbc-ui.com](https://wbc-ui.com)
- **GitHub**: [github.com/nicofr83/wbc-ui2](https://github.com/nicofr83/wbc-ui2)
- **Markdown demo**: [md.wbc-ui.com](https://md.wbc-ui.com)
- **Routing demo**: [wbRoutes2.wbc-ui2.com](https://wbRoutes2.wbc-ui2.com)

---

*wb-core: Build smarter, not harder.*

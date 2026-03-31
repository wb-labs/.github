# Getting Started with wb-core

A quick-start guide to get `wbc-ui2` (the wb-core engine) running in your Vue 2 project.

---

## 1. Install

```bash
npm install wbc-ui2 vue@^2.7 vuetify@^2.7 vuex@^3.6 vue-router@^3.5
```

Include Material Design Icons (not bundled):

```html
<link href="https://cdn.jsdelivr.net/npm/@mdi/font@7.x/css/materialdesignicons.min.css" rel="stylesheet">
```

## 2. Initialize the Plugin

In your `main.js`:

```javascript
import Vue from 'vue';
import Vuetify from 'vuetify';
import WbcUi2Plugin from 'wbc-ui2';
import 'wbc-ui2/dist/style.css';

const vuetifyInst = new Vuetify();

Vue.use(WbcUi2Plugin, {
  plugins: [
    { name: 'Vuetify', property: '$vuetify', fallback: Vuetify, fallbackInstance: vuetifyInst }
  ],
  resolveFile: (path) => path,   // configure file resolution for your bundler
  lg: 'en'                       // default language
});

new Vue({
  vuetify: vuetifyInst,
  render: (h) => h(App)
}).$mount('#app');
```

For Pro users, add your license key:

```javascript
Vue.use(WbcUi2Plugin, {
  premiumKey: 'ABCD-1234-EFGH-5678',
  // ...rest of config
});
```

## 3. Use the `<WBC>` Component

The `<WBC>` component is globally registered after `Vue.use()`. Use it anywhere in your templates.

### Render a string

```html
<WBC item="Hello, world!" />
```

### Render a Markdown file

```html
<WBC item="./docs/readme.md" />
```

### Render a dynamic component from an object

```html
<template>
  <WBC :item="card" />
</template>

<script>
export default {
  data: () => ({
    card: {
      comp: 'VCard',
      title: 'My Card',
      options: {
        class: 'pa-4',
        style: 'max-width: 400px'
      }
    }
  })
}
</script>
```

### Render a list of items

```html
<WBC :item="['First item', './image.png', { comp: 'VBtn', title: 'Click me' }]" />
```

## 4. Reactive Mode with `dive=true`

When `dive` is set to `true`, every property of the item becomes a function of the component state:

```html
<template>
  <WBC :item="reactiveCard" />
</template>

<script>
export default {
  data: () => ({
    reactiveCard: {
      dive: true,
      comp: (that) => that.data.active ? 'VChip' : 'VBtn',
      title: (that) => `Status: ${that.data.active ? 'ON' : 'OFF'}`,
      options: {
        on: {
          click: (that) => that.set(!that.data.active, 'active')
        }
      }
    }
  })
}
</script>
```

The `that` parameter is the `itemAccessebility` proxy -- your controlled interface to the WBC engine.

## 5. Use as a Vue Router Component

WBC works as a route component for dynamic content routing:

```javascript
const routes = [
  { path: '/docs', component: WBC, props: { item: './docs/index.md' } },
  { path: '/dashboard', component: WBC, props: { item: dashboardConfig } }
];
```

## 6. Build Variants

Choose the right build for your setup:

| Variant | Size (gzip) | Best for |
|---|---|---|
| Standard (`wbc-ui2.es.js`) | 49 KB | Production apps (you manage deps) |
| Full-Embed (`wbc-ui2.full-embed.umd.js`) | ~2.6 MB | CDN demos, quick prototypes |

For the full-embed variant, no `style.css` import is needed -- styles are inlined.

## 7. Starter Templates

Clone a template to get started immediately:

- **Vite**: `wb-core_template_vite`
- **Vue CLI**: `wb-core_template_cli`
- **Webpack**: `wb-core_template_webpack`

## Next Steps

- Read the full documentation at [wbc-ui.com](https://wbc-ui.com)
- Explore the Markdown demo at [md.wbc-ui.com](https://md.wbc-ui.com)
- See routing patterns at [wbRoutes2.wbc-ui2.com](https://wbRoutes2.wbc-ui2.com)
- Review the [technical reference](../technical.md) for the full `itemAccessebility` API
- Review the [monetization guide](../monetization.md) to understand Free vs Pro features

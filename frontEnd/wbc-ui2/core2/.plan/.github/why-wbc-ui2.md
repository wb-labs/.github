# Why WBC-UI2? The Case for UI-as-Data

## The Problem

Every UI change today follows the same painful cycle:
**Designer > Developer > PR > Code Review > CI/CD > Deploy > CDN Invalidation**

Want to move a button? That's a 2-5 day process. Want to A/B test a layout? Fork the codebase. Want to let a product manager tweak a dashboard? Hire another frontend developer.

**What if UI was just... data?**

---

## The WBC-UI2 Approach

WBC-UI2 is a **JSON-driven UI rendering engine** for Vue.js. Instead of writing HTML templates, you define your entire UI as data objects — and the engine renders them into fully reactive Vue components.

### Traditional Way

```html
<v-card>
  <v-card-title>Hello World</v-card-title>
  <v-btn @click="save">Save</v-btn>
</v-card>
```

### The WBC-UI2 Way

```json
{
  "comp": "v-card",
  "options": {
    "items": [
      { "comp": "v-card-title", "options": { "html": "Hello World" } },
      { "comp": "v-btn", "options": { "on": { "click": "save" }, "html": "Save" } }
    ]
  }
}
```

**Same result. But now that JSON can come from anywhere:**
- A REST API
- A headless CMS (Strapi, Contentful)
- A database
- An AI model (Claude, GPT)
- A visual builder
- A configuration panel edited by non-developers

---

## Who Is This For?

### Enterprise Teams
- Let product managers change page layouts **without deploying**
- Maintain 50 white-label clients with **one codebase + 50 JSON configs**
- Ship UI changes across all platforms **simultaneously**

### Startups
- Build admin dashboards in **hours instead of weeks**
- Prototype entire interfaces from JSON — iterate without touching code
- Start free, upgrade to Pro when you need advanced orchestration

### AI-Powered Applications
- Your AI generates a JSON UI config > WBC-UI2 renders it live
- No compilation, no deployment, no developer review needed for layout changes
- The natural rendering backend for AI-generated interfaces

---

## What's Included

| Package | What It Does |
|---------|-------------|
| `wbc-ui2` | Core rendering engine — JSON to reactive Vue components |
| `@wbc-ui2/code` | Syntax highlighting and code preview |
| `@wbc-ui2/chart` | Data visualization (ECharts integration) |
| `@wbc-ui2/mermaid` | Text-to-diagram rendering |
| `@wbc-ui2/latex` | Mathematical formula rendering (KaTeX) |
| More coming... | Table, GIS, Data Viewer |

---

## Quick Start

```bash
npm install wbc-ui2
```

```javascript
import Vue from 'vue';
import WBC from 'wbc-ui2';

Vue.use(WBC);
```

```html
<WBC :item="{ comp: 'v-btn', options: { html: 'Hello from JSON!' } }" />
```

That's it. Your first JSON-driven component is live.

---

## Free vs Pro

| | Free | Pro |
|---|---|---|
| Core rendering | Yes | Yes |
| Basic lifecycle hooks (init, updater) | Yes | Yes |
| Advanced orchestration (setup, tracker, logic) | - | Yes |
| Framework access (store, router, refs) | - | Yes |
| Headless content extraction | - | Yes |
| AES-256 encryption utilities | - | Yes |
| Priority support | - | Yes |

The free tier is production-ready. Pro unlocks the full power of the orchestration engine.

---

## Learn More

- [Live Demo](https://demo.wbc-ui.com)
- [Documentation](https://wbc-ui.com)
- [npm](https://www.npmjs.com/package/wbc-ui2)
- [GitHub](https://github.com/wb-labs)

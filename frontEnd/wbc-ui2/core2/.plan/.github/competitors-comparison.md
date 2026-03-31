# WBC-UI2 vs The Competition — An Honest Comparison

## The Landscape

The "UI from data" space is growing fast. Here's where WBC-UI2 sits relative to existing solutions.

---

## Side-by-Side Comparison

| Feature | WBC-UI2 | Form.io | JSON Forms | Amis (Baidu) | Retool | Builder.io |
|---------|---------|---------|------------|--------------|--------|------------|
| **Scope** | Full-page UI | Forms only | Forms only | Full-page UI | Full apps | Visual CMS |
| **Architecture** | npm library | Library + SaaS | Library | Library | Platform | Platform |
| **Framework** | Vue 2 (Vue 3 coming) | Framework-agnostic | React/Vue/Angular | React | Proprietary | Framework-agnostic |
| **Self-hosted** | Yes | Yes (limited) | Yes | Yes | Yes (Enterprise) | No |
| **Open Source** | MIT (core) | Partial | Yes (Apache 2.0) | Yes (Apache 2.0) | No | Partial |
| **npm installable** | Yes | Yes | Yes | Yes | No | Yes |
| **Embed in existing app** | Yes | Yes | Yes | Difficult | No | Yes |
| **Plugin ecosystem** | Yes (charts, maps, code, LaTeX) | Limited | Limited | Built-in | Built-in | Limited |
| **AI-ready (JSON in/out)** | Yes | Partial | Yes | Yes | No | Partial |
| **Pricing** | Free + Pro tiers | Free + $200-300/mo | Free | Free | $10-120/user/mo | Free + paid |

---

## What Each Solution Does Best

### Form.io
Best for: **Complex form workflows** (insurance, healthcare, government)
- Mature form builder with drag-and-drop editor
- Strong workflow engine for multi-step submissions
- **Limitation**: Cannot render arbitrary UI — only form fields

### JSON Forms (Eclipse Foundation)
Best for: **Standards-based form rendering**
- Uses JSON Schema (a recognized standard)
- Framework-agnostic with React, Vue, and Angular renderers
- **Limitation**: Limited to form elements. No page layouts, no component composition.

### Amis (Baidu)
Best for: **Full-page JSON-to-UI in Chinese-speaking markets**
- Closest concept to WBC-UI2: entire pages defined as JSON
- Massive adoption in China (10K+ GitHub stars)
- **Limitation**: Documentation entirely in Chinese. React-only. Not adopted in Western markets.

### Retool / Appsmith
Best for: **Internal tool building** (admin panels, dashboards)
- Full platforms with visual editors, database connectors, auth
- **Limitation**: Closed platforms. Cannot be `npm install`-ed into an existing app. You build inside their environment.

### Builder.io
Best for: **Visual CMS-driven page building**
- Beautiful visual editor that outputs structured data
- Framework-agnostic rendering
- **Limitation**: SaaS platform. You depend on Builder.io's servers. Vendor lock-in.

---

## Where WBC-UI2 Wins

### The Unique Position

```
                    Forms Only <-----------------------------> Full Page UI
                         |                                          |
   Library (npm install) |  JSON Forms    [  WBC-UI2  ]            |
                         |  Form.io                                 |
                         |                                          |
   Platform (hosted)     |  Typeform      Retool    Appsmith        |
                         |                Builder.io                |
```

**WBC-UI2 is the only solution that is simultaneously:**
1. Open-source (MIT)
2. Installable via npm into existing projects
3. Full-page rendering (not forms-only)
4. Runtime interpretation (not compile-time code generation)
5. Has a plugin ecosystem (charts, maps, code, LaTeX, diagrams)
6. Self-hosted (no vendor dependency)

### The Key Differentiators

**1. It lives inside YOUR codebase**
Unlike Retool or Builder.io, WBC-UI2 is a library you import. Your code, your infrastructure, your deployment pipeline.

**2. Full UI, not just forms**
Unlike Form.io or JSON Forms, you can define entire page layouts, navigation, component trees — not just input fields.

**3. Plugin architecture**
Need charts? `npm install @wbc-ui2/chart`. Need diagrams? `npm install @wbc-ui2/mermaid`. Each domain is a plugin. The ecosystem grows independently.

**4. AI-native**
JSON is the natural output format for AI models. WBC-UI2 can render AI-generated interfaces with zero compilation step.

---

## Honest Limitations

| What We're Working On | Status |
|:---|:---|
| Vue 3 support | In development (Q3-Q4 2026) |
| TypeScript definitions | Planned |
| Visual config builder | Planned (2027) |
| React/Svelte support | On the roadmap |
| SSR/SSG support | Not yet available |

We believe in transparency. WBC-UI2 is a growing project — not a finished platform. If you need a mature, enterprise-ready solution today, Retool or Form.io may be better fits. If you want to invest in the future of JSON-driven UI, we're building it.

---

## Try It

```bash
npm install wbc-ui2
```

- [Live Demo](https://demo.wbc-ui.com)
- [Documentation](https://wbc-ui.com)
- [GitHub](https://github.com/wb-labs)

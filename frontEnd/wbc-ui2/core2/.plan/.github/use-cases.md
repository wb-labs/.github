# WBC-UI2 — Real-World Use Cases

## Who Benefits from JSON-Driven UI?

The biggest tech companies have already answered this question. Airbnb, Netflix, Spotify, and DoorDash all built proprietary server-driven UI systems. WBC-UI2 brings the same concept to everyone as an open-source library.

---

## Use Case 1: Enterprise Internal Tools

**The problem**: Every layout change requires a developer, a PR, and a deployment.

**With WBC-UI2**: Product managers edit a JSON configuration. The dashboard updates instantly. No code changes, no deployments.

```json
{
  "comp": "v-container",
  "options": {
    "items": [
      { "comp": "v-row", "options": { "items": [
        { "comp": "WBChart", "options": { "type": "line", "data": "/api/metrics" } },
        { "comp": "WBTable", "options": { "source": "/api/users" } }
      ]}}
    ]
  }
}
```

**ROI**: Replace 3 frontend developers ($390K/year) with 1 developer + 2 config editors ($250K/year). The tool pays for itself in weeks.

---

## Use Case 2: White-Label SaaS

**The problem**: You have 50 clients who each want a "slightly different" UI. You're maintaining 50 branches or building a brittle theming system.

**With WBC-UI2**: One codebase. One deployment. 50 JSON configs — one per client.

```
Client A: /configs/client-a.json  -> Blue theme, 3-column layout
Client B: /configs/client-b.json  -> Green theme, sidebar navigation
Client C: /configs/client-c.json  -> Custom dashboard with charts
```

Each client gets a unique experience from a single deployed application.

---

## Use Case 3: AI-Powered Interface Generation

**The problem**: AI can generate code, but that code still needs to be reviewed, committed, and deployed.

**With WBC-UI2**: AI generates a JSON UI config. The engine renders it immediately. No compilation needed.

```
User: "Create a dashboard with a line chart showing revenue and a table of recent orders"

AI outputs JSON -> WBC-UI2 renders it live -> User sees the result in seconds
```

This makes WBC-UI2 the natural **rendering backend for AI-generated UIs**.

---

## Use Case 4: Form-Heavy Applications

**The problem**: Insurance, healthcare, and government applications have complex multi-step forms that change with regulations. Every change requires a release cycle.

**With WBC-UI2**: Forms are defined as JSON. When regulations change, update the config file. Audit trail built in.

**Context**: Form.io charges $25,000-$100,000+/year for this capability. WBC-UI2 offers a broader solution at a fraction of the cost.

---

## Use Case 5: Content Management

**The problem**: Headless CMS platforms store content as structured data, but page layouts are still hardcoded in templates.

**With WBC-UI2**: The CMS stores both content AND layout as JSON. Content editors control not just what appears on the page, but how it's arranged.

**Integration**: Works naturally with Strapi, Contentful, Sanity, or any headless CMS that serves JSON.

---

## Use Case 6: Mobile Server-Driven UI

**The problem**: Mobile app updates take 1-7 days for App Store review. You can't ship UI changes quickly.

**With WBC-UI2 (future)**: The app fetches its UI definition from your API. Layout changes are instant — no app store review needed.

Airbnb's "Ghost Platform" proved this approach at scale. WBC-UI2 brings it to the open-source ecosystem.

---

## The Common Thread

All these use cases share one insight: **when UI is data, everything gets faster**.

| Traditional | JSON-Driven |
|:---|:---|
| UI changes require developers | Config editors can handle it |
| Every change needs deployment | Changes are instant |
| Per-client customization = code forks | Per-client customization = JSON files |
| AI output needs human review | AI output renders directly |
| Form changes wait for release cycles | Form configs update immediately |

---

## Get Started

```bash
npm install wbc-ui2
```

- [Live Demo](https://demo.wbc-ui.com)
- [Documentation](https://wbc-ui.com)

# WB-MERMAID: Roadmap & Vision

## Mission

Provide a reactive, tiered diagramming component powered by Mermaid.js that renders flowcharts, sequence diagrams, GANTT charts, and more from simple text definitions within the WBC-UI2 ecosystem.

## Current State (v2 -- Vue 2 / JavaScript)

- `WBMermaid.vue` component wrapping Mermaid.js with reactive `item` data binding.
- Tier-gated features: sequence diagrams, GANTT charts, custom themes/configs.
- Public access limited to basic flowcharts; complex diagram types require Pro.
- Distribution: `@wbc-ui2/mermaid` (Free) and `@wbc-ui2/mermaid-pro` (Premium).

## WBC3 Vision (Vue 3 / TypeScript)

### Composable Architecture
- `useMermaid()` -- isolated composable for diagram rendering and theme management.
- `useDiagramParser()` -- typed parser for validating Mermaid syntax before rendering.
- `WBMermaidView` -- pure UI wrapper with error boundary for malformed diagrams.

### Type-Safe Contracts
- `WBMermaidItem` interface with strict typing for `src`, `config`, and `type` properties.
- `WBMermaidAccessibility` context exposing the render pipeline via `ctx.render`.

## Execution Phases

### Phase 1: NPM Distribution
- Publish `@wbc-ui2/mermaid` with peer dependency on `@wbc-ui2/core`.
- Ensure `tiers.mermaid` entry is active in the central store.

### Phase 2: Knowledge Base
- Interactive diagram editor at `wbc-ui.com/mermaid`.
- Live preview playground with side-by-side text/diagram view.

### Phase 3: Ecosystem Scaffolds
- Documentation site template with embedded Mermaid diagrams.
- Architecture documentation starter kit.

### Phase 4: Market Execution
- Technical narrative: "Diagrams as Code: Visual Documentation with WB-MERMAID."
- Comparison with raw Mermaid.js integration effort.

## Success Criteria

- [ ] `npm install @wbc-ui2/mermaid` installs cleanly.
- [ ] Free tier renders basic flowcharts without restrictions.
- [ ] Pro tier unlocks sequence, GANTT, and custom themes.
- [ ] Real-time diagram updates work via the WBC pipe syntax.

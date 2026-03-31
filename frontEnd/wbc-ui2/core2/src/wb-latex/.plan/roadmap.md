# WB-LATEX: Roadmap & Vision

## Mission

Provide a reactive, tiered mathematical typesetting component powered by KaTeX (via vatex) that renders LaTeX expressions within the WBC-UI2 ecosystem, from simple inline math to complex scientific notation with custom macros.

## Current State (v2 -- Vue 2 / JavaScript)

- `WBLatex.vue` component wrapping KaTeX via the vatex engine.
- Tier-gated features: custom macros, bordered styling, advanced color parsing.
- Public access limited to basic math expressions; complex features require Pro.
- Distribution: `@wbc-ui2/latex` (Free) and `@wbc-ui2/latex-pro` (Premium).

## WBC3 Vision (Vue 3 / TypeScript)

### Composable Architecture
- `useKaTeX()` -- isolated composable for expression rendering and error handling.
- `useLatexMacros()` -- macro registry management with validation.
- `WBLatexView` -- pure render wrapper with fallback display for invalid expressions.

### Type-Safe Contracts
- `WBLatexItem` interface with strict typing for `expression`, `macros`, and styling props.
- `WBLatexAccessibility` context for dynamic expression updates via `ctx.render`.

## Execution Phases

### Phase 1: NPM Distribution
- Publish `@wbc-ui2/latex` with peer dependency on `@wbc-ui2/core`.
- Ensure `tiers.latex` entry is active in the central store.

### Phase 2: Knowledge Base
- Interactive formula editor at `wbc-ui.com/latex`.
- Expression gallery with copy-paste examples.

### Phase 3: Ecosystem Scaffolds
- Academic paper template with embedded LaTeX rendering.
- Scientific documentation starter with macro presets.

### Phase 4: Market Execution
- Technical narrative: "Beautiful Math in Vue: The WB-LATEX Story."
- Comparison with raw KaTeX/MathJax integration effort.

## Success Criteria

- [ ] `npm install @wbc-ui2/latex` installs cleanly.
- [ ] Free tier renders basic math expressions without restrictions.
- [ ] Pro tier unlocks custom macros and bordered styling.
- [ ] Real-time expression updates work via the WBC pipe syntax.

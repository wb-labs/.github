# WB-CODE: Roadmap & Vision

## Mission

Provide an intelligence-enabled code editor interface that integrates Monaco/Ace with the WBC-UI2 orchestration engine, transforming raw editors into `item`-driven, tiered smart components.

## Current State (v2 -- Vue 2 / JavaScript)

- Single-file `WBCode.vue` monolith (~6,000 lines) handling Monaco integration, file I/O, and UI.
- Tier-gated features: PDF export, Prettier formatting, deep `ctx.editor` access.
- Distribution: `@wbc-ui2/code` (Free) and `@wbc-ui2/code-pro` (Premium).

## WBC3 Vision (Vue 3 / TypeScript)

### Architectural Shift: Composable/Modular Separation

- `useMonaco()` -- isolated composable for editor initialization and theme management.
- `useEditorLogic()` -- functional core for code execution, search/replace, and snippet handling.
- `WBCodeView` -- pure UI wrapper optimized for performance.

### Type-Safe Contracts

```typescript
interface WBCodeItem {
  code: string;
  language: string;
  filename?: string;
  options?: WBCodeOptions;
  logic?: string | CodeLogicHandler;
}

interface WBCodeAccessibility {
  that: WBCodeInstance;
  ctx: EditorContext;
  run(): void;
  save(): Promise<boolean>;
}
```

## Execution Phases

### Phase 1: NPM Distribution
1. Publish `@wbc-ui2/core` as peer dependency (^1.0.0).
2. Verify `tiers.code` entry is active in the central store.
3. Run `npm run build` and `npm run build:pro`.
4. Publish free version via `npm publish --access public`.

### Phase 2: Knowledge Base
- API reference at `wbc-ui.com/code`.
- Markdown playground at `md.wbc-ui.com`.
- Routing demo at `wbRoutes2.wbc-ui2.com`.

### Phase 3: Ecosystem Scaffolds
- Public demo repository for simple/complex editor implementations.
- Pre-configured Vite template: `gh:wbc-ui/template-code-vite`.

### Phase 4: Market Execution
- Technical narrative: "From Plain-Text to Smart Objects: The WB-CODE Story."
- Dev.to and LinkedIn deep-dives on the architecture.

### Phase 5: WBC3 Migration
1. Formalize `WBCodeItem` types to eliminate runtime props errors.
2. Extract Monaco-specific configuration into `WBC-CORE`.
3. Implement Composition API bridge for Vue 3 compatibility.

## Success Criteria

- [ ] `npm install @wbc-ui2/code` installs cleanly.
- [ ] `WBC_SIMULATE_PRO` unlocks PDF export icon in demo.
- [ ] Automated Prettier formatting active for Pro license holders.
- [ ] Maintenance overhead reduced by 40% through modular testing.

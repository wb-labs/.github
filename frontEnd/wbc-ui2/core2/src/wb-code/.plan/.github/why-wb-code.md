# Why WB-CODE?

## The Problem

You want to embed a code editor in your Vue application. Monaco and Ace are powerful, but integrating them properly means writing hundreds of lines of boilerplate: instance management, theme switching, toolbar wiring, export logic, and state synchronization. Every project reinvents this wheel.

## The Solution

**WB-CODE** (`@wbc-ui2/code`) wraps Monaco/Ace into a single, `item`-driven Vue component. One object configures the entire editor -- language, content, behavior, and appearance.

```vue
<WBCode :item="{ code: myCode, language: 'javascript' }" />
```

That is a working editor. No manual instance setup. No lifecycle management.

## What Makes It Different

- **Item-driven architecture**: pass a single `item` object instead of managing dozens of props and events.
- **Logic injection**: attach runtime behavior via `init(ctx)` and `logic(ctx)` hooks without modifying the component.
- **Built-in Prettier**: Pro tier includes automated HTML/CSS/JS formatting with zero configuration.
- **PDF export**: generate code-to-PDF output directly from the editor toolbar.
- **Unified licensing**: shares the same tier system (`@wbc-ui2/core`) as all WBC-UI2 components.

## Who Is It For

- **Frontend developers** building documentation sites, playgrounds, or admin panels that need embedded code editing.
- **Teams** that want consistent editor behavior across multiple applications without duplicating setup code.
- **Product builders** who need export capabilities (PDF, source) without integrating third-party tools.

## Get Started

```bash
npm install @wbc-ui2/code @wbc-ui2/core
```

```javascript
import { WBCode } from '@wbc-ui2/code';

export default {
  components: { WBCode }
};
```

See the [Getting Started guide](getting-started.md) for a complete setup walkthrough.

# Why WB-MERMAID?

## The Problem

Technical documentation needs diagrams -- flowcharts, sequence diagrams, architecture overviews. Mermaid.js solves the "diagrams as code" problem, but integrating it into a Vue application still requires manual initialization, DOM management, re-rendering logic, and error handling for malformed syntax.

## The Solution

**WB-MERMAID** (`@wbc-ui2/mermaid`) wraps Mermaid.js into a reactive Vue component. Write your diagram in text, pass it as an `item`, and the component renders it automatically.

```vue
<WBMermaid :item="{
  src: 'graph TD; A-->B; B-->C; C-->A;'
}" />
```

Text in, diagram out. No DOM manipulation. No manual re-renders.

## What Makes It Different

- **Reactive rendering**: change the `src` text and the diagram updates instantly. No manual `mermaid.init()` calls.
- **Item-driven**: a single `item` prop configures the entire diagram. Consistent with all WBC-UI2 components.
- **Error resilience**: malformed Mermaid syntax is handled gracefully instead of breaking the page.
- **Tiered complexity**: basic flowcharts are free. Sequence diagrams, GANTT charts, and custom themes are available via Pro.
- **Pipe integration**: diagrams can be dynamically updated through the WBC pipe architecture for real-time applications.

## Who Is It For

- **Documentation authors** embedding architecture diagrams directly in Vue-based docs sites.
- **Technical teams** maintaining living diagrams that update as systems evolve.
- **Product managers** creating process flows and timelines within internal dashboards.
- **Educators** building interactive materials with visual explanations.

## Get Started

```bash
npm install @wbc-ui2/mermaid @wbc-ui2/core
```

```javascript
import { WBMermaid } from '@wbc-ui2/mermaid';
export default { components: { WBMermaid } };
```

See the [Getting Started guide](getting-started.md) for a complete setup walkthrough.

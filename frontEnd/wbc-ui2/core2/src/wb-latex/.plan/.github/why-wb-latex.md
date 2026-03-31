# Why WB-LATEX?

## The Problem

Rendering mathematical notation in web applications is surprisingly hard. KaTeX is fast and beautiful, but integrating it into Vue means managing rendering lifecycles, handling expression errors, and building custom styling around raw math output. MathJax is heavier and slower. Neither gives you a reactive, component-driven experience out of the box.

## The Solution

**WB-LATEX** (`@wbc-ui2/latex`) wraps KaTeX into a reactive Vue component via the vatex engine. Pass a LaTeX expression as an `item` and get beautifully rendered math.

```vue
<WBLatex :item="{ expression: 'E = mc^2' }" />
```

One prop. Instant rendering. Reactive updates when the expression changes.

## What Makes It Different

- **Reactive expressions**: change the `expression` string and the math re-renders instantly. No manual KaTeX calls.
- **Item-driven**: consistent with all WBC-UI2 components. One `item` object configures everything.
- **Error resilience**: invalid LaTeX expressions display gracefully instead of crashing the component.
- **Custom macros (Pro)**: define reusable macros for complex notation like `\R`, `\N`, or domain-specific symbols.
- **Styled containers (Pro)**: the `bordered` prop wraps expressions in polished, presentation-ready containers.
- **Pipe integration**: expressions can be dynamically updated through the WBC pipe for interactive applications.

## Who Is It For

- **Academic platforms** rendering formulas in course materials, papers, or exam interfaces.
- **Scientific dashboards** displaying computed results with proper mathematical notation.
- **Documentation sites** that need inline and block math alongside regular content.
- **Educational apps** building interactive math exercises with real-time feedback.

## Get Started

```bash
npm install @wbc-ui2/latex @wbc-ui2/core
```

```javascript
import { WBLatex } from '@wbc-ui2/latex';
export default { components: { WBLatex } };
```

See the [Getting Started guide](getting-started.md) for a complete setup walkthrough.

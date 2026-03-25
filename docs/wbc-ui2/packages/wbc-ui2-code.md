# @wbc-ui2/code

**@wbc-ui2/code** is the code engine for the WBC-UI2 ecosystem. It provides advanced code rendering, live editing capabilities, and technical document orchestration.

## Features

- **Live Code Execution** — Render and execute code snippets in real-time.
- **Multi-language Support** — Powered by PrismJS for syntax highlighting.
- **WBC Integration** — Full integration with `wbc-ui2` core engine.
- **Export to PDF** — Built-in support for generating PDF documents from code content.

## Installation

```bash
npm install @wbc-ui2/code
```

Requires `wbc-ui2` as a peer dependency.

## Usage

```javascript
import Vue from 'vue';
import WBCUI2 from 'wbc-ui2';
import WBCode from '@wbc-ui2/code';

Vue.use(WBCUI2);    // Core must be installed first
Vue.use(WBCode);    // Then the code extension
```

## Build Formats

| File | Format | Use Case |
| :--- | :--- | :--- |
| `wb-code.es.js` | **ESM** | Modern bundlers |
| `wb-code.umd.js` | **UMD** | CDN / script tags |

## Dependencies

- **Peer**: `vue` (^2.7.0), `wbc-ui2` (^1.0.0)
- **Direct**: `html2pdf.js`, `prismjs`

## Live Demo

- **Documentation**: [wbcode2.wbc-ui.com](https://wbcode2.wbc-ui.com)

## License

MIT

# @wbc-ui2/code

<p align="center">
  <img src="../logo/wb-code.png" alt="WB-Code Logo" width="180"/>
</p>

**@wbc-ui2/code** is the code engine for the WBC-UI2 ecosystem. It provides advanced code rendering, live editing capabilities, and technical document orchestration.

## Features

- **Live Code Execution**: Render and execute code snippets in real-time.
- **Multi-language Support**: Powered by PrismJS for syntax highlighting.
- **WBC Integration**: Full integration with `wbc-ui2` core engine.
- **Export to PDF**: Built-in support for generating PDF documents from code content.

## Installation

Install via npm:

```bash
npm install @wbc-ui2/code
```

Requires `wbc-ui2` as a peer dependency.

## Available Formats

- **ESM**: `dist/wb-code.es.js`
- **UMD**: `dist/wb-code.umd.js`

## Usage

```javascript
import Vue from 'vue';
import wbcCode from '@wbc-ui2/code';

Vue.use(wbcCode);
```

## Dependencies

- **Peer**: `vue` (^2.7.0), `wbc-ui2` (^0.0.1)
- **Direct**: `html2pdf.js`, `prismjs`

## License

MIT

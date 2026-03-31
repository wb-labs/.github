# WB-LATEX: Getting Started

## Installation

```bash
npm install @wbc-ui2/latex @wbc-ui2/core
```

## Register the Plugin

```javascript
import Vue from 'vue';
import WbCore from '@wbc-ui2/core';
import WbLatex from '@wbc-ui2/latex';

Vue.use(WbCore);
Vue.use(WbLatex);
// For Pro features: Vue.use(WbLatex, { premiumKey: 'YOUR_KEY' });
```

## Basic Usage

```vue
<template>
  <WBLatex :item="mathItem" />
</template>

<script>
export default {
  data() {
    return {
      mathItem: {
        expression: '\\int_{0}^{\\infty} e^{-x^2} dx = \\frac{\\sqrt{\\pi}}{2}'
      }
    };
  }
};
</script>
```

## Pro Features (Macros & Styling)

```javascript
mathItem: {
  expression: '\\R^n \\to \\R^m',
  macros: { '\\R': '\\mathbb{R}' },
  bordered: true
}
```

## Local Testing

```javascript
Vue.use(WbLatex, { premiumKey: 'WBLatex_SIMULATE_PRO' });
```

# WB-CODE: Getting Started

## Installation

```bash
npm install @wbc-ui2/code @wbc-ui2/core
```

## Register the Plugin

```javascript
import Vue from 'vue';
import WbCore from '@wbc-ui2/core';
import WbCode from '@wbc-ui2/code';

Vue.use(WbCore);
Vue.use(WbCode);
// For Pro features: Vue.use(WbCode, { premiumKey: 'YOUR_KEY' });
```

## Basic Usage

```vue
<template>
  <WBCode :item="editorItem" />
</template>

<script>
export default {
  data() {
    return {
      editorItem: {
        code: 'console.log("Hello, world!");',
        language: 'javascript'
      }
    };
  }
};
</script>
```

## Pro Features (Logic Injection)

```javascript
editorItem: {
  code: '/* start coding */',
  language: 'html',
  logic(ctx) {
    ctx.format();              // auto-format with Prettier
    ctx.exportPDF();           // generate PDF from editor content
    console.log(ctx.editor);   // raw Monaco/Ace instance
  }
}
```

## Local Testing with Simulated Pro

```javascript
Vue.use(WbCode, { premiumKey: 'WBC_SIMULATE_PRO' });
```

This unlocks all Pro features locally without a license key.

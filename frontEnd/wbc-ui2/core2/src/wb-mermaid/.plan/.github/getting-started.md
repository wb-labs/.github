# WB-MERMAID: Getting Started

## Installation

```bash
npm install @wbc-ui2/mermaid @wbc-ui2/core
```

## Register the Plugin

```javascript
import Vue from 'vue';
import WbCore from '@wbc-ui2/core';
import WbMermaid from '@wbc-ui2/mermaid';

Vue.use(WbCore);
Vue.use(WbMermaid);
// For Pro features: Vue.use(WbMermaid, { premiumKey: 'YOUR_KEY' });
```

## Basic Usage (Flowchart)

```vue
<template>
  <WBMermaid :item="diagramItem" />
</template>

<script>
export default {
  data() {
    return {
      diagramItem: {
        src: `graph TD
          A[Start] --> B{Decision}
          B -->|Yes| C[Action]
          B -->|No| D[End]`
      }
    };
  }
};
</script>
```

## Pro Features (Sequence Diagrams, GANTT)

```javascript
diagramItem: {
  src: `sequenceDiagram
    Alice->>Bob: Hello
    Bob-->>Alice: Hi back`,
  config: { theme: 'forest' }
}
```

## Local Testing

```javascript
Vue.use(WbMermaid, { premiumKey: 'WBMermaid_SIMULATE_PRO' });
```

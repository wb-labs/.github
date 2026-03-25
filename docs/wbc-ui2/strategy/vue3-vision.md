# WBC-UI3: The TypeScript & Vue 3 Migration Blueprint

> **Goal**: Transition from a JS-based Vue 2 UI Engine to a high-performance, type-safe Vue 3 ecosystem while preserving the "One-Object" architecture.

---

## 1. Core Architecture Shift: Composition API

In WBC-UI2, logic resides in a single large engine file. In WBC-UI3, we use **Composables** to separate concerns:

```
/src
  /composables
    useWbcMeta.ts           # Logic for resolving nameEl, key, and options
    useWbcPermissions.ts    # Centralized Pro/Free/Dev logic
    useWbcRender.ts         # The rendering engine (v-node generation)
    useWbcAccessibility.ts  # Building the 'that' object
  WBC.vue                   # Simple entry point using <script setup>
```

## 2. TypeScript: The Enterprise Value Multiplier

Providing Type Definitions allows Pro users to get full autocomplete in VS Code:

```typescript
interface WbcItem {
  comp?: string | Component;
  title?: string;
  options?: WbcOptions;
  children?: WbcItem[];
  // Lifecycle Hooks
  init?: (that: ItemAccessibility) => void;
  tracker?: (that: ItemAccessibility) => void;
  logic?: (that: ItemAccessibility) => void;
}

interface ItemAccessibility {
  userTier: 'free' | 'premium' | 'development';
  data: any;
  props: Record<string, any>;
  emit: (event: string, ...args: any[]) => void;
  // Premium only
  root?: any;
  vm?: any;
  store?: any;
}
```

## 3. The Pro Guard System

Using Vite's `define` and **Dynamic Imports** for clean tree-shaking:

```typescript
const setupProFeatures = async (acc: ItemAccessibility) => {
  if (__WBC_PRO__) {
    const { attachProCapabilities } = await import('./pro/engine');
    attachProCapabilities(acc);
  }
}
```

## 4. Performance: Proxy-based Reactivity

| | Vue 2 | Vue 3 |
| :--- | :--- | :--- |
| **Reactivity** | `Object.defineProperty` (expensive) | `Proxy` (handles 10,000+ nested objects) |
| **Root Nodes** | Single root required | Fragments (multiple roots) |
| **Tree-Shaking** | Limited | Native ESM, full tree-shaking |

## 5. Tiered Feature Split

| Feature | Base (Free/MIT) | Pro (Enterprise) |
| :--- | :--- | :--- |
| **Meta-Rendering** | Standard Components | + Custom Logic Injections |
| **Data Binding** | 1-Way | + 2-Way (Complex Validations) |
| **Headless** | ❌ | ✅ Full `that.content` extraction |
| **Type Safety** | Basic types | ✅ Full Internal Access Interfaces |

## 6. Execution Roadmap

| Phase | Timeline | Objective |
| :--- | :--- | :--- |
| **Phase 1: Typing** | Month 1 | `.d.ts` file for the Vue 2 version as Pro Bonus |
| **Phase 2: Composables** | Month 2 | Move `itemAccessebility` into independent TS functions |
| **Phase 3: Vue 3 Bridge** | Month 3 | `vue-demi` compatibility for both Vue 2 and Vue 3 |

---

**Why this sells?** You aren't buying a "Vue 2 hack." You are buying a **State-of-the-Art TypeScript Framework** that happens to support legacy migration.

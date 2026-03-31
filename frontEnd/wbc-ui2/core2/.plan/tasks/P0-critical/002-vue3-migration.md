# TASK: Vue 3 Migration

**Priority**: P0 (Critical — Existential)
**Effort**: 3-6 months full-time
**Status**: Not Started (vision documented in roadmap.md)

---

## Why This Is Existential

Vue 2 reached EOL in December 2023. No enterprise evaluates a Vue 2-only library in 2026. Every month without Vue 3 support shrinks the addressable market.

## Migration Scope

| Current (Vue 2) | Target (Vue 3) | Impact |
|:---|:---|:---|
| Options API | Composition API (`<script setup>`) | Full rewrite of WBC.js |
| Vuex 3 | Pinia | Store refactor |
| `Object.defineProperty` | Proxy-based reactivity | Performance gain |
| Single root required | Fragments | Simplification |
| Bootstrap-Vue | No Vue 3 port — find alternative | Breaking change |
| Vuetify 2 | Vuetify 3 (different API) | Component config changes |
| JavaScript | TypeScript | New type system |

## Phased Approach

### Phase 1: Type Foundation (Month 1)
- [ ] Publish `.d.ts` for current Vue 2 version (Pro bonus)
- [ ] Define core TypeScript interfaces (`WbcItem`, `ItemAccessibility`)
- [ ] JSON Schema specification for config format

### Phase 2: Decomposition (Month 2)
- [ ] Split WBC.js (5,750 lines) into composables:
  - `useWbcMeta.ts` — nameEl, key, options resolution
  - `useWbcPermissions.ts` — Pro/Free/Dev logic
  - `useWbcRender.ts` — rendering engine
  - `useWbcAccessibility.ts` — building the `that` object
- [ ] Split utils.js (2,906 lines) into focused modules

### Phase 3: Vue 3 Bridge (Month 3)
- [ ] Evaluate `vue-demi` for dual Vue 2/3 support
- [ ] Migrate one sub-package as a proof-of-concept
- [ ] Document migration guide for users

### Phase 4: Full Migration (Month 4-6)
- [ ] Core engine rewrite with Composition API
- [ ] Vuex to Pinia migration
- [ ] Vuetify 2 to Vuetify 3
- [ ] Bootstrap-Vue replacement decision
- [ ] Update all 50+ apps

## Risks
- Bootstrap-Vue has no Vue 3 version — may need to drop or replace
- Vuetify 3 API is significantly different — component configs will break
- Must maintain Vue 2 version during transition period

# TASK: Fix `itemAccessebility` Typo

**Priority**: P2 (Normal — but do it before Vue 3 release)
**Effort**: 1-2 hours (+ migration guide)
**Status**: Not Started

---

## Problem

The core API uses `itemAccessebility` (typo) instead of `itemAccessibility`. This is baked into the entire codebase.

## Actions

- [ ] Global rename: `itemAccessebility` -> `itemAccessibility`
- [ ] Update all documentation
- [ ] Add a deprecation alias for backward compatibility during transition
- [ ] Document in changelog as a breaking change
- [ ] Best timing: do this as part of Vue 3 migration (breaking change anyway)

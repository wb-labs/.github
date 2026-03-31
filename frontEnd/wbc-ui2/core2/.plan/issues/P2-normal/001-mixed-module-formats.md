# ISSUE: Mixed ES6 and CommonJS Imports

**Severity**: P2 (Normal)
**Location**: Various files in `wb-core/src/`
**Reported**: 2026-03-30 (audit)

---

## Description

Mixed ES6 `import` and CommonJS `require()` in the same files. This causes issues with tree-shaking and can lead to subtle bugs with module resolution.

## Fix
- Standardize on ES6 imports throughout
- Address during Vue 3 migration

# TASK: WBC.js Decomposition

**Priority**: P1 (High)
**Effort**: 2-4 weeks
**Status**: Not Started

---

## Problem

`WBC.js` is 5,750 lines doing rendering, state management, media detection, file loading, code highlighting, validation, drag/drop, meta tags, and caching — all in one component. This is unmaintainable.

## Target Structure

Split into focused modules (<500 lines each):

```
wb-core/src/
├── WBC.js              # Entry point (~200 lines) — component definition, props, lifecycle
├── engine/
│   ├── renderer.js     # VNode generation, component resolution
│   ├── fileHandler.js  # File loading, extension detection, pipe parsing
│   ├── accessibility.js # itemAccessebility proxy construction
│   ├── tiering.js      # Free/Pro/Dev feature gating
│   ├── toggles.js      # toggleLoad, toggleHide, toggleDrag, etc.
│   ├── media.js        # Image/video/audio detection and rendering
│   └── validation.js   # Form validation, isValid, isValidFn
├── utils.js            # Split into focused utility modules
├── constants.js        # Unchanged
└── index.js            # Unchanged
```

## Rules
- Each module exports pure functions or small objects
- No module should exceed 500 lines
- Maintain backward compatibility — public API unchanged
- Write tests for each new module as it's extracted

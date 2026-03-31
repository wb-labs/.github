# TASK: Automated Testing Setup

**Priority**: P1 (High)
**Effort**: 2-3 months (ongoing)
**Status**: Not Started

---

## Problem

Zero automated tests across 17,000+ lines of core code. Every change risks regressions with no safety net. Every `package.json` has `"test": "echo Error"`.

## Actions

### 1. Framework Setup (Week 1)
- [ ] Install Vitest as test runner
- [ ] Configure test environment for Vue 2 components
- [ ] Set up code coverage reporting
- [ ] Add `npm test` scripts to root and each package

### 2. Core Engine Tests (Week 2-4)
- [ ] Unit tests for `utils.js` helper functions (pure functions, easy wins)
- [ ] Unit tests for store getters/mutations (tier detection, license flow)
- [ ] Component tests for `<WBC>` rendering:
  - String items
  - Object items with `comp`
  - Array items
  - File path resolution
  - Pipe syntax parsing
- [ ] Tier gating tests (free vs pro behavior)

### 3. Sub-Package Tests (Week 5-8)
- [ ] `@wbc-ui2/code` — rendering, syntax detection
- [ ] `@wbc-ui2/chart` — ECharts integration, tier gating
- [ ] `@wbc-ui2/mermaid` — diagram rendering
- [ ] `@wbc-ui2/latex` — formula rendering

### 4. CI/CD Pipeline (Week 1, parallel)
- [ ] GitHub Actions workflow: lint + test + build on every PR
- [ ] Code coverage badge in README
- [ ] Block merges on test failure

## Target
- 60%+ code coverage on core engine within 3 months
- All new code must include tests

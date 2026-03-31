# ISSUE: Silent Error Catches

**Severity**: P1 (High)
**Location**: Throughout `WBC.js` and sub-packages
**Reported**: 2026-03-30 (audit)

---

## Description

Multiple `catch(e) {}` blocks throughout the codebase silently swallow errors. This makes debugging extremely difficult and can mask real issues in production.

## Fix
- Replace empty catches with proper error logging
- Add error boundaries for component rendering
- Consider a centralized error handler via the store

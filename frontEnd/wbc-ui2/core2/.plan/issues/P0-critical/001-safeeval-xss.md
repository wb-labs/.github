# ISSUE: safeEval() + innerHTML = XSS Vulnerability

**Severity**: P0 (Critical)
**Location**: `wb-core/src/WBC.js` (safeEval), `wb-core/src/components/WBHtml.vue` (innerHTML)
**Reported**: 2026-03-30 (audit)

---

## Description

`safeEval()` uses `new Function()` with attempted variable masking. This is bypassable and enables arbitrary code execution. Combined with 8+ raw `innerHTML` assignments without sanitization, this creates a direct XSS attack vector.

Any application built with WBC-UI2 inherits these vulnerabilities.

## Impact
- Any user-supplied JSON config can execute arbitrary JavaScript
- Any rendered HTML content can inject scripts
- Disqualifying for enterprise adoption

## Fix
See [tasks/P0-critical/001-security-hardening.md](../tasks/P0-critical/001-security-hardening.md)

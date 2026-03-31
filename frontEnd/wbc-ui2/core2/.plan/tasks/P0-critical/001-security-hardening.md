# TASK: Security Hardening

**Priority**: P0 (Critical)
**Effort**: 1-2 weeks
**Status**: Not Started

---

## Problem

Two critical security vulnerabilities block any enterprise adoption:

1. **`safeEval()` uses `new Function()`** — exploitable for arbitrary code execution. Attempts to mask `window`, `document`, `fetch`, `localStorage` but this is bypassable.
2. **Raw `innerHTML` without DOMPurify** — 8+ instances across `WBHtml.vue` and `utils.js`. Direct XSS vector.

## Actions Required

### 1. Replace `safeEval()`
- [ ] Audit all call sites of `safeEval()` in `WBC.js`
- [ ] Replace with a proper sandboxed evaluation (e.g., `expression-eval`, `mathjs`, or remove entirely)
- [ ] If dynamic code execution is needed, use a strict allowlist of permitted operations

### 2. Add DOMPurify
- [ ] `npm install dompurify`
- [ ] Wrap all `innerHTML` assignments: `el.innerHTML = DOMPurify.sanitize(content)`
- [ ] Audit: `WBHtml.vue`, `utils.js` (grep for `innerHTML`)
- [ ] Ensure markdown output is also sanitized

### 3. Additional Security
- [ ] Add CSP headers to all deployed demo apps
- [ ] Add X-Frame-Options headers
- [ ] Audit `.env` files — remove any committed API keys
- [ ] Review cookie-based license for CSRF protection

## Success Criteria
- No `new Function()` in production builds
- All innerHTML assignments go through DOMPurify
- Zero XSS vectors detectable by automated scanning

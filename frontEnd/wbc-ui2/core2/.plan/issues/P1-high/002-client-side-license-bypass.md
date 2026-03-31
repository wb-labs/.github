# ISSUE: License Validation is Client-Side Only

**Severity**: P1 (High)
**Location**: `wb-core/src/store/index.js`, cookie-based checks
**Reported**: 2026-03-30 (audit)

---

## Description

License validation is a client-side cookie check. Any developer can bypass it in 30 seconds by setting the cookie manually. No server-side validation exists.

## Impact
- Premium features can be unlocked without payment
- No telemetry to detect unauthorized use
- Reduces enterprise trust in the product

## Fix
- Implement server-side license validation endpoint
- Use signed tokens (JWT) instead of plain cookies
- Add periodic re-validation (phone-home)
- Estimated effort: 2-3 weeks

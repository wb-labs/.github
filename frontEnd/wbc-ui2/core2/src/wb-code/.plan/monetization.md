# WB-CODE: Monetization & Licensing

## Tier Model

### Free Tier (`@wbc-ui2/code`)
- Standard code editor (Monaco/Ace) with basic syntax highlighting.
- Reactive `item` data binding (1-way).
- Standard Light/Dark themes.
- Basic `init(ctx)` hook access.
- `toggleTheme()`, `emit()`, basic `toggleToolbar()`.

### Pro Tier (`@wbc-ui2/code-pro`)
- **Logic injection**: full `logic(ctx)` and `init(ctx)` orchestration hooks.
- **Toolbar icons**: `pdfCode`, `pdfComp` unlocked.
- **Automated Prettier** formatting for HTML, CSS, and JS.
- **Deep editor access**: raw Monaco/Ace API via `ctx.editor`.
- **PDF export**: `exportPDF()` for code-to-PDF generation.
- **Raw Vue instance**: `ctx.vm` for deep framework access.
- **Precision toolbar control**: fine-grained `toggleToolbar(v)`.

## Licensing Flow

### Trigger: `created()` in `WBCode.vue`

1. Check for existing cookie `_wbc_code_auth`.
2. If found, hydrate store via `setTierStatus({ pkg: 'code', authorized: true })`.
3. If `premiumKey: 'WBC_SIMULATE_PRO'` is passed, bypass API check.
4. Otherwise, perform LemonSqueezy API ping for validation.
5. Refresh cookie with 24h timestamp.

### Persistence

| Parameter | Value |
|---|---|
| Cookie Name | `_wbc_code_auth` |
| Store Slug | `code` |
| Max Age | 86400 (24 hours) |
| SameSite | `Lax` |

## Architecture: Build-Time Enforcement

- **Free build** (`wb-code.js`): PDF export library and Prettier formatting logic are physically stripped by `vite-plugin` during production builds.
- **Pro build** (`wb-code-pro.js`): Full feature set included.
- **Runtime gating**: `ctx` object constructor checks `isPackageAuthorized('code') || __DEV__` before attaching sensitive properties like `ctx.editor`.
- **Dev bypass**: `__DEV__` (via `serve_vite`) grants full access regardless of license.

## Feature Gating Summary

| Feature | Free | Pro | Dev |
|---|:---:|:---:|:---:|
| `code` (get/set text) | Yes | Yes | Yes |
| `editor` (raw instance) | No | Yes | Yes |
| `format()` (Prettier) | No | Yes | Yes |
| `exportPDF()` | No | Yes | Yes |
| `logic(ctx)` hook | No | Yes | Yes |
| `tracker(ctx)` hook | No | Yes | Yes |
| `vm` (Vue instance) | No | Yes | Yes |
| `toggleWbCode(v)` | No | No | Yes |

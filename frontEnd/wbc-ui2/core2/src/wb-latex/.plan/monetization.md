# WB-LATEX: Monetization & Licensing

## Tier Model

### Free Tier (`@wbc-ui2/latex`)
- Standard LaTeX expression rendering via KaTeX (vatex engine).
- Reactive `item` data binding via `expression` property.
- Basic math typesetting with default KaTeX styling.
- `itemAccessebility` level 0 access.

### Pro Tier (`@wbc-ui2/latex-pro`)
- **Custom macros**: full `macros` prop access for reusable KaTeX macro definitions.
- **Bordered styling**: the `bordered` prop enables styled container wrappers for highlighted expressions.
- **Advanced color logic**: `colorIsTextColor` for sophisticated color parsing.
- **Dynamic rendering**: real-time expression updates via `ctx.render` through the WBC bridge.

## Licensing Flow

### Trigger: `created()` in `WBLatex.vue`

1. Check for existing cookie `_wb_latex_auth`.
2. If found and valid (under 24h), hydrate `tiers.latex` state.
3. If `premiumKey: 'WBLatex_SIMULATE_PRO'` is passed, bypass API check.
4. Otherwise, ping LemonSqueezy API for validation.
5. Commit status and details to the global WBC-CORE store.

### Persistence

| Parameter | Value |
|---|---|
| Cookie Name | `_wb_latex_auth` |
| Store Slug | `latex` |
| Max Age | 86400 (24 hours) |
| SameSite | `Lax` |

## Architecture: Build-Time Enforcement

- **Runtime gating**: `$store.state.tiers.latex.authorized` checked in `created()`.
- **UI enforcement**: unauthorized users see a "Lock" state for premium expressions.
- **Dev bypass**: `__DEV__` grants full access regardless of license.

## Feature Gating Summary

| Feature | Free | Pro | Dev |
|---|:---:|:---:|:---:|
| Basic math expressions | Yes | Yes | Yes |
| Custom macros | No | Yes | Yes |
| Bordered styling | No | Yes | Yes |
| `colorIsTextColor` | No | Yes | Yes |
| `ctx.render` access | No | Yes | Yes |

# WB-MERMAID: Monetization & Licensing

## Tier Model

### Free Tier (`@wbc-ui2/mermaid`)
- Standard flowchart rendering from Mermaid text syntax.
- Reactive `item` data binding via `src` property.
- Basic diagram output with default Mermaid theme.
- `itemAccessebility` level 0 access.

### Pro Tier (`@wbc-ui2/mermaid-pro`)
- **Complex diagram types**: sequence diagrams, GANTT charts, class diagrams, state diagrams.
- **Custom configuration**: full `config` prop access for Mermaid theme and layout customization.
- **Dynamic rendering**: real-time diagram updates via `ctx.render` through the WBC pipe.
- **Deep access**: full control over Mermaid engine configuration.

## Licensing Flow

### Trigger: `created()` in `WBMermaid.vue`

1. Check for existing cookie `_wb_mermaid_auth`.
2. If found and valid (under 24h), hydrate `tiers.mermaid` state.
3. If `premiumKey: 'WBMermaid_SIMULATE_PRO'` is passed, bypass API check.
4. Otherwise, ping LemonSqueezy API for validation.
5. Commit status and details to the global WBC-CORE store.

### Persistence

| Parameter | Value |
|---|---|
| Cookie Name | `_wb_mermaid_auth` |
| Store Slug | `mermaid` |
| Max Age | 86400 (24 hours) |
| SameSite | `Lax` |

## Architecture: Build-Time Enforcement

- **Runtime gating**: `$store.state.tiers.mermaid.authorized` checked in `created()`.
- **UI enforcement**: unauthorized users see a "Lock" state or limited diagram complexity.
- **Dev bypass**: `__DEV__` grants full access regardless of license.

## Feature Gating Summary

| Feature | Free | Pro | Dev |
|---|:---:|:---:|:---:|
| Flowcharts | Yes | Yes | Yes |
| Sequence diagrams | No | Yes | Yes |
| GANTT charts | No | Yes | Yes |
| Custom themes/config | No | Yes | Yes |
| `ctx.render` access | No | Yes | Yes |

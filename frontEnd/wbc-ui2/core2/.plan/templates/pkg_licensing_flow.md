# [PKG]: Licensing Flow & Implementation Detail (Pattern)

> **Definition**: This document serves as the mandatory template for defining the particular validation flow of a package's license (hooks, cookies, and store hydration).

---

## 1. Validation Logic Hook (`created`)
Document where the validation logic is housed (usually within the primary component's `created()` hook).

### Standard Flowsteps:
1.  **Persistence Recovery**: Attempt to load session details from the local cookie (`_wbc_[pkg]_auth`).
2.  **Simulation Check**: Detect if the `premiumKey` is the simulation override (`WBC_SIMULATE_PRO`).
3.  **Network Validation**: If required, perform an asynchronous ping to the licensing API.
4.  **State Hydration**: Commit the authorized status and user details to the unified `tiers` object in the store.

---

## 2. Persistence Configuration
Define the specific cookie and store parameters for this package.

| Parameter | Pattern |
|---|---|
| **Cookie Name** | `_wbc_[pkg]_auth` |
| **Store Slug** | `[pkg_slug]` |
| **Persistence Period** | 86400 seconds (24 hours) |

---

## 3. Tiered Feature Gating
Define which high-level component capabilities are locked by this validation flow.
*   **Restricted Methods**: (e.g., `exportPDF()`, `deepIntrospection()`).
*   **Restricted Hooks**: (e.g., `setup()`, `tracker()`).
*   **Access Overlays**: Conditional rendering of premium-only badges or blockers.

---

## 4. Development Bypass Logic
Every licensing flow MUST implement the **"God Mode" Bypass**:
*   If `__DEV__` is true (Owner mode), the validation flow is skipped, and the store is immediately authorized.

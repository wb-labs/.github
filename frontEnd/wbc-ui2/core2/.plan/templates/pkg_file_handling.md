# [PKG]: File Handling & Processing Strategy (Pattern)

> **Definition**: This document serves as the mandatory template for defining how a package dynamically detects, parses, and renders various file types.

---

## 1. Detection Heuristics (Heuristic Flow)
Define the strategy for identifying file types (e.g., by extension, by content analysis, or by module export check).

### Detection Flowchart (Pattern)
1.  **Phase 1 (Identity)**: Check extension (`.js`, `.json`, `.[Pkg_Ext]`).
2.  **Phase 2 (Content)**: Regex-based or internal marker check (e.g., `@wbc-marker`).
3.  **Phase 3 (Module)**: Check for specific function or object exports (e.g., `init`, `logic`).

---

## 2. Supported Extensions & Tiered Handling
Classify the handling of different extensions by user tier.

| Extension | Free Handling | Premium (Pro) Handling | Description |
|---|---|---|---|
| **.[Pkg_Ext]** | [Basic Render] | [Advanced/Logic] | Primary package extension. |
| **.js / .ts** | [Script Snippet] | [Logic Provider] | Orchestration logic. |
| **.json** | [Static Display] | [Reactive Data] | Data-driven rendering. |

---

## 3. Advanced Syntax & Pipe Support (Pro Feature)
Document any advanced inline syntax for file handling (e.g., the `|` pipe syntax).

**Format Pattern:**
`item="[FilePath] | [CSS] | [Param] | [Explicit_Parser]"`

---

## 4. Programmatic Data Layer ([PKG] Content)
Define how raw content is exposed within the `ctx` object for premium users (e.g., headless extraction).

### Data Schema (Template)
*   `input`: Raw file contents and metadata.
*   `output`: Transformed VNodes, processed HTML, or structured JSON.

---

## 5. Tiering & God Mode Enforcement
*   **Feature Gating**: Document which parsers or extraction methods are locked behind the Pro tier.
*   **Dev Bypass**: Document "God Mode" behavior (e.g., full architectural access regardless of license).

# WBC-UI2 Apps & Demos Directory

All live applications, documentation portals, and starter templates in the `@wbc-ui2` ecosystem.

---

## 📦 WB-CORE

| Type | App Name | Live URL |
| :--- | :--- | :--- |
| 🏠 Official Site | wbc-ui.com | [wbc-ui.com](https://wbc-ui.com) |
| 🚀 Live Demo | Core Demo | [demo.wbc-ui.com](https://www.demo.wbc-ui.com) |
| 📝 Markdown Demo | md.wbc-ui.com | [md.wbc-ui.com](https://md.wbc-ui.com) |
| 🔀 Routing Demo | wbRoutes2.wbc-ui2.com | [wbRoutes2.wbc-ui2.com](https://wbRoutes2.wbc-ui2.com) |
| 📖 WB-Press Docs | wb-press.wbc-ui2.com | [wb-press.wbc-ui2.com](https://wb-press.wbc-ui2.com) |
| 📋 Starter Template | Vite | *Available in monorepo* |
| 📋 Starter Template | Webpack | *Available in monorepo* |
| 📋 Starter Template | Vue CLI | *Available in monorepo* |

---

## 💻 WB-CODE

| Type | App Name | Live URL |
| :--- | :--- | :--- |
| 📖 Documentation | wbcode2.wbc-ui.com | [wbcode2.wbc-ui.com](https://wbcode2.wbc-ui.com) |
| 🚀 Live Demo | Code Demo | [wbcode2.wbc-ui.com](https://wbcode2.wbc-ui.com) |
| 📋 Starter Templates | Vite / Webpack / CLI | *Available in monorepo* |

---

## 📊 WB-CHART

| Type | App Name | Live URL |
| :--- | :--- | :--- |
| 📖 Documentation | wb-chart.wbc-ui.com | [wb-chart.wbc-ui.com](https://wb-chart.wbc-ui.com) |
| 🚀 Live Demo | Chart Demo | [wb-chart.wbc-ui.com](https://wb-chart.wbc-ui.com) |
| 📋 Starter Templates | Vite / Webpack / CLI | *Available in monorepo* |

---

## 📐 WB-MERMAID

| Type | App Name | Live URL |
| :--- | :--- | :--- |
| 📖 Documentation | wb-mermaid.wbc-ui.com | [wb-mermaid.wbc-ui.com](https://wb-mermaid.wbc-ui.com) |
| 🚀 Live Demo | Mermaid Demo | [wb-mermaid.wbc-ui.com](https://wb-mermaid.wbc-ui.com) |
| 📋 Starter Templates | Vite / Webpack / CLI | *Available in monorepo* |

---

## 🧪 WB-LATEX

| Type | App Name | Live URL |
| :--- | :--- | :--- |
| 🚀 Live Demo | LaTeX Demo | *Coming soon* |
| 📋 Starter Templates | Vite / Webpack / CLI | *Available in monorepo* |

---

## Monorepo Structure

The codebase is organized as a npm workspaces monorepo:

```
core2/
├── wb-core/            # wbc-ui2 — The Core Engine
├── wb-code/            # @wbc-ui2/code
├── wb-chart/           # @wbc-ui2/chart
├── wb-latex/           # @wbc-ui2/latex
├── wb-mermaid/         # @wbc-ui2/mermaid
├── wb-table/           # @wbc-ui2/table (coming soon)
├── wb-gis/             # @wbc-ui2/gis (coming soon)
├── wb-dataviewer/      # @wbc-ui2/wbDataviewer (coming soon)
├── wbc-wiki-obj/       # Sample data and wiki
├── wb-vuepressThemeWb2/# VuePress theme for docs portals
├── apps/               # All demos, docs portals, and starter templates
└── package.json        # Root monorepo manifest
```

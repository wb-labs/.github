# WBC-UI2 CLI — Scaffolding Architecture & Usage Guide

The **`@wbc-ui2/cli`** (invoked as `wb`) is the primary orchestration tool for the WBC-UI2 ecosystem. It provides a standardized, interactive experience for bootstrapping new projects and premium components.

---

## 1. Architecture

Built on a "Commander + Inquirer" pattern:

- **Entry Point**: `wb-cli/wb.js` (using `commander`)
- **Command Modules**: `wb-cli/commands/` (using `inquirer`)
- **Templates**: Integrated into command logic, mirrors latest `wb-core` and `wb-code` standards
- **Fallback**: Built-in `readline` prompt in `wb-cli/prompt.js`

---

## 2. Installation

### Option A: Local Linking (Development)

```bash
cd src/wb-cli
sudo npm link
```

### Option B: npm Global

```bash
npm install -g @wbc-ui2/cli
```

---

## 3. Commands

### `wb init` — Project Scaffolding

Scaffolds a new Vue 2 / WBC-UI2 application:
1. **Version Selection**: Choose ecosystem version
2. **Component Picker**: Multi-select premium packages (Table, Code, GIS, etc.)
3. **Tool Configuration**: Toggle ESLint, Prettier, SASS
4. **Auto-Installation**: Optionally runs `npm install` immediately

### `wb create <PkgName>` — Package Scaffolding

Bootstraps new premium modules within the monorepo:
1. Generates standardized folder structure (`src/`, `.plan/`)
2. Injects the monorepo-standard `created()` hook for licensing
3. Optionally generates roadmap and technical flow placeholders

### `wb help` — Documentation

Displays detailed documentation for all commands and options.

---

## 4. Troubleshooting

**"wb: command not found" (Error 127)**:
1. Ensure `sudo npm link` was run inside `wb-cli/`
2. Verify global npm binary path is in `$PATH`
3. Run `npm bin -g` to find the correct installation path

---

*Consolidated from: `technical/pkg_cli_scaffolding_architecture.md`*

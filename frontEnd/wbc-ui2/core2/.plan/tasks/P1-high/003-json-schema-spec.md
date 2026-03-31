# TASK: JSON Schema Specification

**Priority**: P1 (High)
**Effort**: 2-4 weeks
**Status**: Not Started

---

## Problem

The JSON config format is proprietary and undocumented as a specification. Users must learn the API by reading source code. No IDE tooling, no JSON Schema validation, no autocomplete support.

## Actions

- [ ] Define JSON Schema for `WbcItem` config objects
- [ ] Publish schema to SchemaStore for IDE auto-detection
- [ ] Generate TypeScript types from schema
- [ ] VS Code extension for config validation and autocomplete
- [ ] Document the schema in public docs

## Example Schema (Draft)

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "comp": { "type": "string", "description": "Vue component name" },
    "title": { "type": "string" },
    "html": { "type": "string" },
    "options": { "$ref": "#/$defs/WbcOptions" },
    "items": {
      "type": "array",
      "items": { "$ref": "#" }
    }
  }
}
```

# Figma Design System Skills

Two Codex skills for Figma design-system work:

- `figma-audit-design-system`
- `figma-extract-design-system`

These skills are designed for teams working in Figma who want stricter review and extraction workflows for design systems.

## Included Skills

### `figma-audit-design-system`

Use this skill when a design system already exists and needs structure or naming cleanup.

Typical use cases:

- audit category grouping
- normalize spec layout
- fix title and canvas mismatches
- clean up duplicate naming
- check whether screens are actually consuming the design system

### `figma-extract-design-system`

Use this skill when source screens exist but a reusable design system has not been properly extracted yet.

Typical use cases:

- review source screens before componentization
- classify what should become foundations, icons, primitives, and composed components
- propose `To Add / To Modify / Do Not Extract`
- extract and rebind the resulting design system

## Repo Structure

```text
.
├── figma-audit-design-system/
│   ├── SKILL.md
│   ├── agents/
│   └── references/
└── figma-extract-design-system/
    ├── SKILL.md
    ├── agents/
    └── references/
```

## Install

Clone this repo, then copy one or both skills into your local Codex skills directory:

```bash
cp -R figma-audit-design-system ~/.codex/skills/
cp -R figma-extract-design-system ~/.codex/skills/
```

If the directories already exist, replace them intentionally:

```bash
rm -rf ~/.codex/skills/figma-audit-design-system
rm -rf ~/.codex/skills/figma-extract-design-system
cp -R figma-audit-design-system ~/.codex/skills/
cp -R figma-extract-design-system ~/.codex/skills/
```

## Requirements

- Codex with local skill loading enabled
- Figma MCP configured and available to Codex

## Notes

- Both skills assume a Figma-capable environment.
- `figma-extract-design-system` is extraction-first and review-first.
- `figma-audit-design-system` is audit-first and normalization-first.
- No license file has been added yet. Choose one before publishing publicly if you want explicit reuse terms.

# Figma Design System Skills

Reusable Codex skills for reviewing, extracting, and normalizing Figma design systems.

This repo currently includes two skills:

- `figma-audit-design-system`
- `figma-extract-design-system`

They are intended for teams that want more structured Figma workflows than a generic "make components from this file" prompt.

## What These Skills Do

### `figma-audit-design-system`

Use this when a design system already exists, but its structure needs review or cleanup.

Good fit for:

- category grouping audits
- spec layout normalization
- title and canvas mismatch cleanup
- duplicate naming cleanup
- semantic layer naming cleanup
- checking whether product screens are actually using the design system

### `figma-extract-design-system`

Use this when source screens exist but the design system has not been cleanly extracted yet.

Good fit for:

- reviewing source screens before componentization
- separating foundations, icons, primitive components, and composed components
- deciding what should not be extracted
- producing a `To Add / To Modify / Do Not Extract` review
- extracting the resulting design system in the right order
- rebinding source screens after extraction

## Skill Philosophy

These skills deliberately avoid "componentize everything" behavior.

They bias toward:

- understanding structure first
- preserving reusable boundaries
- excluding page-only layout and decoration
- keeping naming and spec presentation coherent
- rebinding screens after extraction instead of stopping at component creation

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

Clone the repo:

```bash
git clone https://github.com/chelswcs/codexskill.git
cd codexskill
```

Copy one or both skills into your local Codex skills directory:

```bash
cp -R figma-audit-design-system ~/.codex/skills/
cp -R figma-extract-design-system ~/.codex/skills/
```

If you are replacing existing local copies, remove the old ones first:

```bash
rm -rf ~/.codex/skills/figma-audit-design-system
rm -rf ~/.codex/skills/figma-extract-design-system
cp -R figma-audit-design-system ~/.codex/skills/
cp -R figma-extract-design-system ~/.codex/skills/
```

## Requirements

- Codex with local skill loading enabled
- Figma MCP configured and available to Codex

## Suggested Usage

Use `figma-extract-design-system` when starting from real product screens.

Use `figma-audit-design-system` after a library already exists and needs cleanup, validation, or normalization.

In practice, a common workflow is:

1. extract from source screens
2. rebind the screens
3. audit the resulting library

## License

MIT

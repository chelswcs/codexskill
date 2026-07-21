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
- recording source evidence, confidence levels, and unresolved decisions
- rebinding screens after extraction instead of stopping at component creation
- validating rebinding with before/after screenshots before accepting swaps

## Expected Outputs

Each skill should leave a short handoff trail, not only make Figma changes.

For extraction work, expect:

- reviewed scope and source frames
- reusable patterns found
- `To Add / To Modify / Do Not Extract`
- source trace and confidence rating for important component decisions
- implementation order
- before/after screenshot validation for rebinding
- rebinding and validation summary
- unresolved risks or follow-up pass

For audit work, expect:

- audited scope
- mismatch list grouped by issue type with confidence ratings
- fixes applied in small batches
- re-audit result, including any unpassed items and reasons
- remaining raw screen usage or naming debt
- next recommended pass

## Repo Structure

```text
.
├── figma-audit-design-system/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── audit-checklist.md
│       ├── audit-report-template.md
│       ├── common-fixes.md
│       └── confidence-levels.md
└── figma-extract-design-system/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── confidence-levels.md
        ├── library-rules.md
        ├── review-template.md
        └── workflow.md
```

`confidence-levels.md` is duplicated in both skills on purpose: skills are installed
independently into `~/.codex/skills/`, so a shared cross-folder reference would break
after install. Keep the two copies in sync.

## Install

Clone the repo:

```bash
git clone https://github.com/chelswcs/figma-ds-workflows.git
cd figma-ds-workflows
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

## Usage Examples

### Example: extract from product screens

Use this when you already have one or more Figma screens and want to turn them into a reusable design system.

```text
Use $figma-extract-design-system on this Figma file.
Review the workout, dashboard, and profile screens first.
Identify foundations, icons, primitive components, and composed components.
Before creating anything, give me:
- To Add
- To Modify
- Do Not Extract
Then extract the system in the correct order and rebind the source screens.
```

### Example: audit an existing library

Use this when the design system already exists but its structure or naming quality is inconsistent.

```text
Use $figma-audit-design-system on this Figma design system page.
Inspect category titles, spec titles, canvas structure, and component naming.
Find duplicate labels, mismatched titles, and generic layer names.
Apply the fixes in small batches, then re-audit the updated sections.
```

### Example: check if screens are actually using the library

This is useful when a team has components in the file, but some screens may still contain raw frames instead of bound instances.

```text
Use $figma-audit-design-system to inspect these product screens and tell me which areas are still raw layout instead of design-system instances.
Group findings by:
- raw screen usage issue
- instance/title mismatch
- category mismatch
Then fix the obvious rebinding problems.
```

## Recent Updates

These skills were hardened against a full extract → rebind → audit run on a real
product file. Changes from that pass:

- **Fixed the Figma MCP endpoint** in both `agents/openai.yaml` — it previously
  pointed at an unrelated MCP server, so the skills could not reach Figma at all.
- **Confidence levels with an independence rule** (`confidence-levels.md`): state
  copies, duplicated frames, and repeated rows count as one occurrence, not several,
  and contradictory patterns are capped and surfaced instead of silently resolved.
- **Rebinding is mandatory, not optional.** Every source screen must end rebound or
  explicitly rolled back with a reason, validated by before/after screenshots — the
  extraction is not "done" while screens are left raw.
- **Handoffs land as files.** Review and handoff reports are written to `reports/`,
  and may only claim what is checkable against the Figma file.
- **Role-based typography taxonomy.** Text styles are organized by role
  (`Heading / Title / Body / Numeric / Nav / Action / Input / Label`), not by font
  family; `Label` is reserved for sub-14px annotations; structural exceptions
  (navigation, inputs, buttons) get their own role folder tagged `EXCEPTION`.
- **Uppercase is typed into the characters**, never encoded in a style's `textCase`
  (which silently detaches on override and hides the real content).
- **Single source of truth for styles.** Documented styles must be the same objects
  components actually consume, and every documented style must map to at least one
  visible element.

## License

MIT

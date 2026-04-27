---
name: figma-extract-design-system
description: Extract a reusable design system from existing Figma screens. Use when the task is to review source screens, identify foundations, icons, primitive components, and composed components, decide what should not be extracted, propose a build plan, then create and rebind the resulting design system in Figma.
---

# Figma Extract Design System

Use this skill when the goal is to turn one or more existing Figma screens into a reusable design system.

Do not start by creating components. Start by understanding structure.

This skill requires a Figma write-enabled session.

Before any write step, confirm that `mcp__figma__use_figma` is available in the current session.
If `use_figma` is not available, stop at analysis and review only. Do not pretend write steps can proceed. Restart in a Figma write-enabled session first.

This skill covers the full extraction workflow:
- review source screens
- classify reusable boundaries
- propose `To Add / To Modify / Do Not Extract`
- build or extend foundations
- extract icons, primitive components, and composed components
- rebind the source screens
- normalize the resulting library

## Workflow

0. Confirm tool surface first.
   - Check that `mcp__figma__use_figma` is available before any write
   - If it is missing, limit the turn to analysis and planning only

1. Read the source screens first.
   Identify layout regions, repeated patterns, icons, foundations, local-only layout, and decorative elements.

2. Classify candidates before building anything.
   Sort findings into:
   - foundations
   - icons
   - primitive components
   - composed components
   - local-only layout
   - decoration / divider / container shapes

3. Exclude what should not be extracted.
   Do not extract:
   - page-only layout wrappers
   - decorative geometry
   - simple dividers
   - background rectangles
   - state or container shapes that have no independent meaning

4. Present a review list before writing.
   Always give the user three lists first:
   - `要新增 / To Add`
   - `要修改 / To Modify`
   - `不該抽 / Do Not Extract`

5. Create foundations before components.
   Build or extend:
   - colors
   - typography
   - spacing
   - radius
   - other project token groups if needed

6. Extract icons before larger components.
   Make icons standalone components first, then let higher-level components consume them.

7. Extract primitive components before composed components.
   Examples:
   - button
   - input
   - chip
   - list item
   - state
   - timer

8. Extract composed components after primitives are stable.
   Examples:
   - tab bar
   - action bar
   - card
   - workout header

9. Rebind the design system back to the original screens.
   Validate that the screens can consume the new components and tokens without visual drift.

10. Normalize the library structure at the end.
   Fix:
   - category grouping
   - spec layout
   - titles
   - canvas structure
   - semantic layer naming

Use these references during the workflow:
- [references/workflow.md](references/workflow.md)
- [references/review-template.md](references/review-template.md)
- [references/library-rules.md](references/library-rules.md)

## Required review output before creation

Before any write, produce:

- scope being reviewed
- reusable patterns found
- foundations needed
- `To Add`
- `To Modify`
- `Do Not Extract`
- proposed implementation order

## Library rules to preserve

When working in a file that already has a design system, match the existing conventions first.

Common conventions from this project:
- `Foundations` and `Components` are separate
- components are grouped by function, not by page
- every preview uses `Spec / ...`
- each spec is `Title` above `Canvas`
- `Canvas` contains the component instance or component set
- visible title text must match the instance/component name shown below
- category titles must describe the instances under that group
- avoid duplicate naming across category title, spec title, and component name

## Validation checklist

After extraction, confirm:
- component names are unique
- spec titles match component names
- canvas contains the correct instance or component set
- category title matches the set of specs below it
- reused screens are actually consuming the design system
- no obvious raw frames remain where a component should exist

---
name: figma-audit-design-system
description: Audit and normalize an existing Figma design system. Use when the task is to review category grouping, spec layout, titles, canvas structure, component naming, semantic layer naming, duplicate labels, or whether a screen is correctly using the design system.
---

# Figma Audit Design System

Use this skill when the design system already exists and the job is to inspect, verify, and fix structure or naming problems.

This is an audit skill, not an extraction-first skill.

This skill requires a Figma write-enabled session for any repair pass.

Before applying fixes, confirm that `mcp__figma__use_figma` is available in the current session.
If `use_figma` is not available, the skill may still perform a read-only audit, but it must stop before any Figma write action and tell the user that a write-enabled session is required.

Before the first fix that writes to the file, remind the user to save a named version in Figma's version history as a restore point, and wait for them to confirm. The plugin API cannot save version history, so the user must do it by hand: File → Save to version history (Cmd/Ctrl+Option+S). A read-only audit needs no restore point; the reminder applies only before write actions.

Use it for:
- category grouping review
- spec layout normalization
- title and canvas alignment
- duplicate naming cleanup
- semantic layer naming cleanup
- checking whether source screens are actually consuming the design system

Use these references during the audit:
- [references/audit-checklist.md](references/audit-checklist.md)
- [references/common-fixes.md](references/common-fixes.md)
- [references/audit-report-template.md](references/audit-report-template.md)
- [references/confidence-levels.md](references/confidence-levels.md)

## Primary audit targets

Review these in order:

1. Category structure
   - does each category title match the specs below it
   - are related components grouped together by function

2. Spec structure
   - `Title` must be above `Canvas`
   - `Canvas` must be below `Title`
   - `Canvas` should use the same auto layout and padding pattern as the rest of the library

3. Title consistency
   - category title content matches the section
   - spec title content matches the component name
   - canvas instance or component set name matches the visible spec title

4. Duplicate naming
   - no repeated visible titles that refer to different components
   - no misleading reused labels such as a button title appearing above unrelated specs

5. Component naming
   - component names are functional and unique
   - no page-based naming unless the project explicitly uses it

6. Semantic layer naming
   - no generic names like `Frame 12`, `Rectangle 1`, `Vector 2`
   - use semantic names by role

7. Screen usage audit
   - determine whether source frames are actually using design system instances
   - identify raw areas that still need to be rebound or extracted

## Audit method

0. Confirm tool surface first.
   - If `mcp__figma__use_figma` is unavailable, do a read-only audit only
   - Only proceed to fixes in a write-enabled Figma session

1. Inspect the page structure first.
2. Compare old, correct sections with new or suspect sections.
3. Identify mismatches before changing anything.
4. Report the mismatches in a short list.
5. Apply fixes in small batches.
6. Re-audit after each batch.
7. End with a handoff report that records fixes, remaining issues, and the next recommended pass.

## Required mismatch categories

When reporting findings, classify them as:
- category mismatch
- spec mismatch
- canvas mismatch
- instance/title mismatch
- duplicate naming
- semantic layer naming issue
- raw screen usage issue

Each finding should include:
- source page / frame / group
- expected structure
- actual mismatch
- proposed fix
- confidence: high, medium, or low

Use [references/confidence-levels.md](references/confidence-levels.md) to assign confidence consistently.

## Fix rules

- Do not rename blindly: renaming is only allowed when there is a corresponding recorded finding with a confidence rating.
- Fix visible content and layer names together.
- If a title is correct but the instance name is wrong, fix the instance name.
- If the instance is correct but the visible title is wrong, fix the visible title.
- If category content and grouping disagree, fix the grouping first, then the title.
- Keep spec layout consistent with the established library pattern.

## Decision prompts

When a decision needs user input, ask with fixed options instead of open-ended questions:

- Before applying a fix batch: `apply this batch / adjust first / skip this batch`
- A finding could be fixed two ways (for example rename the title vs rename the instance): `fix the title / fix the instance / leave and record`
- A low-confidence finding: `confirm and fix / leave and record`

Record the chosen option next to the affected finding in the report file.

## Required final output after audit

After the audit or repair pass, produce:

- audited scope
- mismatch summary by category
- fixes applied
- items intentionally left unchanged
- re-audit result, including any unpassed items and reasons
- remaining raw screen usage or naming debt
- recommended next pass

Write this report to a markdown file in the working directory (for example `reports/ds-audit-report-YYYYMMDD.md`), not only into the chat reply. Only claim what was actually fixed: every claim must be checkable against the Figma file.

## Validation checklist

After an audit pass, confirm:
- every category title matches the specs below it
- every spec title matches its instance/component name
- every canvas shows the correct instance or component set
- `Title` is above `Canvas`
- no duplicate visible spec titles remain
- no generic layer names remain in the audited components
- component masters live inside their spec `Canvas`; no unexplained holding sections such as `_Library Assets`
- structural frames on library pages use auto layout, with no absolutely-positioned scatter or manual spacing
- documented colors and text styles carry usage notes, and no undocumented near-duplicate text styles remain

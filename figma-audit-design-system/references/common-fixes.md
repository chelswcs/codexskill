# Common Fixes

## Category title mismatch

Symptoms:
- Category title content does not describe the specs below it
- Category title appears in the wrong vertical position

Fix:
- Correct the visible text
- Move the category title to the top of the group
- Normalize the first spec offset to match existing groups

## Spec layout mismatch

Symptoms:
- Canvas appears above title
- Spacing differs from the rest of the library

Fix:
- Reorder to `Title -> Canvas`
- Restore the established item spacing and auto layout settings

## Instance / title mismatch

Symptoms:
- Spec title says one component name, canvas shows another

Fix:
- Rename the instance or component when it is wrong
- Rename the visible title when the title is wrong
- Re-audit after the change

## Duplicate visible naming

Symptoms:
- Repeated visible text appears across unrelated specs

Fix:
- Inspect real text nodes, not only frame names
- Compare title text with instance names
- Remove stale or misplaced labels

## Category grouping issue

Symptoms:
- Components under one category clearly belong to another

Fix:
- Fix grouping first
- Then fix category title content
- Then verify spec titles and instance names again

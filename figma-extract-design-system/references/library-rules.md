# Library Rules

Apply the existing design system conventions first.

Project rules established in this file:

- `Foundations` and `Components` are separate
- Components are grouped by function, not by page
- Category title must describe the specs underneath it
- Each spec uses:
  - `Title` above
  - `Canvas` below
  - the canvas preview must match the title text
- Canvas uses auto layout and consistent padding
- Spec titles and component names should align exactly where possible
- Avoid duplicate visible naming across categories, specs, and instances
- Layer naming must be semantic, not tool-default

## One style family, single source of truth

The color/text/effect styles documented on the Foundations page must be the SAME style objects that component masters actually consume. Never create a documentation-only style set in parallel with the styles applied in components — renames and merges on the documented set silently miss production text. Before documenting, inventory what is actually applied; after documenting, verify by node reference that specimens and masters point at identical style IDs. Keep one consistent line-height convention across the whole type scale unless a documented exception exists.

## Typography documentation order and taxonomy

Sort the typography documentation by font family group first, then font size descending, then weight descending (Bold > Semi Bold > Medium > Regular) within the same size. Keep category semantics sharp and stated at the start of each usage note: `Label` styles are captions/annotations, `Numeric` styles are data values that are never uppercased, `Body` is running text, and policy exceptions are tagged `EXCEPTION`. A style whose real usage is data values must be named Numeric even if it started as a Label. Figma SECTION nodes do not auto-resize — after adding specimens, resize the section to fit its documentation frame.

Two hard rules learned from user review:

- Never encode uppercase in a text style's `textCase`. Uppercase is typed directly into the characters; styles keep `textCase: ORIGINAL`. A textCase-based style silently detaches when nodes override text properties, and it hides the real content.
- Every documented style must be bound to at least one VISIBLE element on the actual screens or component masters. Usage that exists only inside hidden layers or collapsed states does not justify a documented style — remove the style or surface the usage.

## Where component masters live

Place the master component or component set directly inside its spec `Canvas` whenever possible, so the spec is the single home of the component. Do not create a separate dump section (such as `_Library Assets`) that holds masters while specs show only instances — it splits the source of truth and confuses readers. If a holding area is genuinely unavoidable, it must carry a visible note explaining what it is and why it exists.

## Layout discipline

Every structural frame on the `Foundations` and `Components` pages must use auto layout: sections, spec frames, `Title`, `Canvas`, and documentation blocks. Do not leave absolutely-positioned scatter, overlapping frames, or hand-nudged spacing. Spacing between specs and between categories must come from consistent auto-layout gaps and padding, not manual positioning.

## Typical categories

These categories come from one example project. Treat them as examples only, and follow the target file's actual conventions when they differ.

- Navigation
  - `Navigation / Tab Bar`
  - `Navigation / Action Bar`
- Buttons
  - `Button / Primary`
  - `Button / Secondary`
- Session
  - reusable workout/session components


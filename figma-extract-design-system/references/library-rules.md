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


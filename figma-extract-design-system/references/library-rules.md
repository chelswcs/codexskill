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

## Typography taxonomy: organize by ROLE, not font family

Users pick a text style by what they are typesetting, not by which font the policy assigns — so the style path names the ROLE and the font family stays out of it. The family is enforced by the font policy note and audits, not by navigation. Rules:

1. Role folders, in display order: `Heading`, `Title`, `Body`, `Numeric`, `Nav`, `Action`, `Input`, `Label` (adapt roles to the project, largest/most prominent first).
2. `Label` is reserved for annotations BELOW 14px. Styles at 14px and above are named by usage context: heading, title, body, display, numeric, and so on.
3. Structural policy exceptions (navigation, inputs, buttons) get their OWN role folder with an `EXCEPTION` tag in the usage note — never bend another role's rules to house them.
4. `Numeric` styles are data values and are never uppercased; a style whose real usage is data values must be classified Numeric even if it started elsewhere.
5. Every usage note starts with its role classification prefix (e.g. `HEADING —`, `DATA VALUE —`, `NAV (EXCEPTION: …) —`).
6. Within each role folder sort by font size descending, then weight descending (Bold > Semi Bold > Medium > Regular). Apply the SAME order to the style panel: folders via `figma.moveLocalTextFolderAfter`, styles via the reverse move-to-front technique (`figma.moveLocalTextStyleAfter` with reference null, iterating the desired order in reverse — chained after-previous moves can leave stragglers). Documentation order and panel order must match.
7. Figma SECTION nodes do not auto-resize — after adding specimens, resize the section to fit its documentation frame.

Two hard rules learned from user review:

- Never encode uppercase in a text style's `textCase`. Uppercase is typed directly into the characters; styles keep `textCase: ORIGINAL`. A textCase-based style silently detaches when nodes override text properties, and it hides the real content.
- Every documented style must be bound to at least one VISIBLE element on the actual screens or component masters. Usage that exists only inside hidden layers or collapsed states does not justify a documented style — remove the style or surface the usage.

## Where component masters live

Place the master component or component set directly inside its spec `Canvas` whenever possible, so the spec is the single home of the component. Do not create a separate dump section (such as `_Library Assets`) that holds masters while specs show only instances — it splits the source of truth and confuses readers. If a holding area is genuinely unavoidable, it must carry a visible note explaining what it is and why it exists.

## Layout discipline

Every structural frame on the `Foundations` and `Components` pages must use auto layout: sections, spec frames, `Title`, `Canvas`, and documentation blocks. Do not leave absolutely-positioned scatter, overlapping frames, or hand-nudged spacing. Spacing between specs and between categories must come from consistent auto-layout gaps and padding, not manual positioning.

## What belongs in the system vs stays in the component

A design system is not a collection of every repeated value — it is a set of shared
decisions meant to hold across screens and states and to keep evolving. Frequency
only proves a value is worth *checking*, not that it must become a token.

A pattern earns a place in the system when it:

- has a stable, understandable meaning across different UI contexts,
- can be safely changed centrally to affect all usages at once,
- supports predictable variation (state, size, responsive, theme),
- removes a repeated design/development decision, and
- has a clear usage scope that is hard to misuse.

If a value belongs to a specific brand, asset, illustration, or data content, keep it
inside its component. Changing it would change the *identity of the content*, not the
system semantics of the interface — e.g. Bitcoin orange or USDC blue are asset
identity, not global UI roles, so they live in the Bitcoin/USDC components, not as
global semantic color tokens.

So a component can be systematized without exposing every internal property as a
variable. Expose the controllable, swappable, extensible parts; encapsulate the
identity-only details. This keeps the global token set small, semantically clear, and
safe to keep extending.

## Persist visual before/after evidence

Before/after screenshots (for rebinding) and in-context crops (for style/merge
decisions) are the evidence a human relies on to approve a change — persist them, do
not leave them as links.

- Figma `get_screenshot` URLs are short-lived, and a "before" state cannot be
  rebuilt once the file changes. Download every capture to a local PNG the moment it
  is taken (e.g. `curl -L -o` into `reports/assets/<pass>-<nodeId>-before.png` /
  `-after.png`), before doing the mutation.
- Name files so a reviewer can pair them: include the pass name, node id, and
  `before`/`after`.
- This lets the reviewer assemble a side-by-side comparison after the run,
  independent of which agent or terminal executed it. A terminal-only agent that can
  only emit text still leaves usable image files behind.

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


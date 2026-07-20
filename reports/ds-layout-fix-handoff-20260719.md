# DS-skill-test layout fix handoff

Date: 2026-07-19  
Figma file: `FkBEN1gq0fSMKe7y1Yor6D` — DS-skill-test  
Audited pages: Foundations `4:64`, Components `4:65`  
Source-screen drift checks: `1:96`, `1:429`, `1:781`, `1:971`

## Scope and constraints

This pass changed layout geometry only. It did not change component semantics, variant property names or values, component-property definitions, instance bindings, or text content. The four source screens were not edited directly.

## Findings and fixes

| Audit category | Finding | Confidence | Fix |
|---|---|---|---|
| canvas mismatch | Component sets retained stale/manual variant offsets, most severely Navigation Header `10:672`. | high | Converted all nine sets to one-row horizontal auto layout with 32px gaps and hugging axes. Preserved every variant's recorded dimensions. |
| canvas mismatch | Color usage notes extended beyond fixed 140px swatch cards. | high | Changed all ten swatches to 240px fixed width and hugging height with 16px padding and 12px gaps. |
| spec mismatch | Component specs exceeded fixed-width `Specs` containers and section bounds. | high | Made Canvas, Spec, Specs, and Section Content structures hug their children; resized sections and arranged them in a non-overlapping grid. |

## Defect 1 — component-set stale offsets

### Navigation Header

| Node | Before | After |
|---|---|---|
| Component set `10:672` | `1440×3034` | `2912×88` |
| `Active=Simple Earn` `9:131` | `x=0, y=0, 1440×88` | `x=0, y=0, 1440×88` |
| `Active=Pro Earn` `10:671` | `x=0, y=2946, 1440×88` | `x=1472, y=0, 1440×88` |
| Canvas `9:134` | `1488×3082` | `2960×136` |
| Spec `9:132` | `1528×3154` | `3000×208` |
| Specs `4:240` | `1720×3154` | `3000×208` |
| Section Content `16:1400` | `1720×3223` | `3000×277` |
| Navigation section `4:238` | `1800×3303` | `3080×357` |

The set is wider because both 1440px variants are now deliberately presented side by side. Its height equals its tallest variant instead of retaining the former canvas offset.

### Strategy Toggle

| Node | Before | After |
|---|---|---|
| Component set `17:576` | `1192×144` | `1112×64` |
| `Context=Modal` `7:103` | `x=40, y=40, 540×64` | `x=0, y=0, 540×64` |
| `Context=Pro Base` `17:571` | `x=612, y=40, 540×64` | `x=572, y=0, 540×64` |
| Canvas `7:106` | `1240×192` | `1160×112` |
| Spec `7:104` | `1280×264` | `1200×184` |
| Controls section `4:232` | `1200×850` | `1280×333` |

### All component sets

All nine sets now use horizontal auto layout, a 32px inter-variant gap, no wrap, and hugging width/height. Every variant was locked back to its recorded pre-fix dimensions after restacking. The APY Tile variants briefly inherited fill sizing during the first restack; they were restored to `182×110` before structural layout or validation. Final APY Tile set `6:210` is `396×110`.

| Component set | Final size | Tallest variant | Height ratio |
|---|---:|---:|---:|
| Button `6:41` | `2905×64` | 64 | 1.00 |
| Asset Selector `6:121` | `1110×77` | 77 | 1.00 |
| Deposit Input `6:175` | `2708×114` | 114 | 1.00 |
| Strategy Toggle `17:576` | `1112×64` | 64 | 1.00 |
| APY Tile `6:210` | `396×110` | 110 | 1.00 |
| Result Row `6:249` | `1466×60` | 60 | 1.00 |
| Navigation Header `10:672` | `2912×88` | 88 | 1.00 |
| Earn Panel `9:526` | `2112×374` | 374 | 1.00 |
| Settlement Panel `9:1125` | `2112×598` | 598 | 1.00 |

## Defect 2 — Foundations clipping

### Color swatches

All ten swatches, including `Swatch / color/bg/canvas` `4:82`, changed from fixed `240×140` to fixed-width/hug-height `240×165`.

For example, Usage Note `16:1234` remains at `y=119`, height `30`, ending at `149`. The card now ends at `165`, leaving the required 16px bottom padding instead of clipping the note by 9px.

| Node | Before | After |
|---|---|---|
| Swatch `4:82` | `240×140`, fixed height, clips content | `240×165`, hug height, no clipping |
| Usage Note `16:1234` | bottom `149` beyond card bottom `140` | bottom `149` within card bottom `165` |
| Color Grid `4:81` | `1040×460` | `1040×535`, fixed wrap width / hug height |
| Documentation `4:67` | `1120×613` | `1120×688`, hug height |
| Colors section `4:66` | `1200×850` | `1200×798`, content plus section padding |

### Other Foundations cards

- All ten typography specimen cards already hugged their content; they were normalized to no clipping and retained their natural heights. Example: Display 64 specimen `4:128` remains `1040×117`, with Usage Note `16:1265` ending at `109` inside the card.
- `Type Specimens` `4:112` is `1040×933` with hug height; Typography Documentation `4:70` is `1120×1086` with hug height.
- Spacing, Radius, and Effects specimen containers retain a fixed 1040px documentation width but hug their heights: `4:143` is `1040×328`, `4:199` is `1040×364`, and `4:218` is `1040×220`.
- All five Foundations sections were resized to contain their documentation and arranged with 100px horizontal and 120px vertical gutters. No overlaps remain.

## Defect 3 — Components overflow and page tidiness

Every Components structure now follows:

`Section Content (vertical hug) → Title + Specs (horizontal hug) → Spec (vertical hug) → Title + Canvas (hug)`

Each section has 40px content padding and was explicitly resized because Figma SECTION nodes do not support auto layout.

Representative overflow repairs:

| Node | Before | After |
|---|---|---|
| Button Spec `6:42` | `1712×278` inside `1120×278` Specs | `2993×184` inside matching `2993×184` Specs `4:228` |
| Buttons Section Content `16:1392` | `1120×347` | `2993×253` |
| Buttons section `4:226` | `1200×850` | `3073×333` |
| Deposit Input Spec `6:176` | `1612×380` inside `1420×838` Specs | `2796×234` inside hugging `4308×234` Specs `4:231` |
| Inputs Section Content `16:1394` | `1420×907` | `4308×303` |
| Inputs section `4:229` | `1500×987` | `4388×383` |

Final Components placement uses two consistent columns:

- Column 1: `x=0` — Icons, Inputs & Selectors, Data Display, Panels.
- Column 2: `x=4632` — Buttons, Controls, Navigation.
- Horizontal and vertical gutters are 120px.
- Section overlap count: 0.

## Mandatory programmatic audit

The final audit was executed through read-only `use_figma`, once per page.

| Metric | Foundations `4:64` | Components `4:65` |
|---|---:|---:|
| Structural frames audited | 55 | 69 |
| Child nodes beyond structural parent frame bounds | **0** | **0** |
| Children beyond SECTION bounds | **0** | **0** |
| Unexpected fixed-size structural frames where hug is expected | **0** | **0** |
| Component sets over 1.5× tallest variant | n/a | **0 of 9** |
| Section overlaps | **0** | **0** |

All nine component-set height ratios are 1.00.

### Intentional fixed sizes

- Foundations Documentation and Title widths remain fixed at 1120px/1040px for a consistent reading column; their heights hug.
- Foundations wrapping grids remain 1040px wide to preserve stable comparison columns; their heights hug.
- Color and typography cards retain consistent fixed widths; their heights hug.
- Spacing, radius, and effect visualization cards retain fixed internal geometry because their dimensions demonstrate the documented token/effect.
- The 18 Components `Title` frames retain fixed widths to align to their containing spec/category columns; all Title heights hug. This is intentional alignment, not overflow.
- Component variant masters retain fixed width and height so restacking the component-set container cannot alter the product components or their source-screen instances.

## Full-page visual verification

| Page | Final capture | Natural screenshot size | Result |
|---|---|---:|---|
| Foundations `4:64` | `https://www.figma.com/api/mcp/asset/0b196855-48b1-4480-9366-7001c07ecb88` | `3800×1943` | All usage notes visible; sections contained and non-overlapping. |
| Components `4:65` | `https://www.figma.com/api/mcp/asset/b64abc56-0ba1-4308-9ce3-b019fac98c8f` | `7712×2910` | Sets tightly stacked; specs contained; two-column layout has no overlaps. |

Screenshot asset URLs are short-lived; node IDs and the audit measurements above are the durable verification references.

## Source-screen drift checks

Each screen was captured before and after. The PNG pairs are byte-for-byte identical, verified by matching SHA-256 hashes.

| Screen | Before capture | After capture | SHA-256 | Result |
|---|---|---|---|---|
| Simple base `1:96` | `https://www.figma.com/api/mcp/asset/beeb06b4-f12b-41a6-acb0-cf907166b34d` | `https://www.figma.com/api/mcp/asset/632e2b07-afe4-40b7-b20a-e5ee6978c4dd` | `0026caedb672340b614d8a3176ccf5b93665ab86b5709c4c9f11860481266d3f` | Pixel-identical; no drift. |
| Simple overlay `1:429` | `https://www.figma.com/api/mcp/asset/c209a17c-e23e-487f-be78-c1da4cedb93b` | `https://www.figma.com/api/mcp/asset/c4a3db81-55cd-49d4-a8aa-fb7c09ded7ff` | `1666e59716e29c6ec355ecdd8ce86f527a4b80b5039bacee54a4efdca3fe8782` | Pixel-identical; no drift. |
| Pro base `1:781` | `https://www.figma.com/api/mcp/asset/e2632670-c39c-4cf9-b5c2-646693a6de2b` | `https://www.figma.com/api/mcp/asset/52cf4fb6-15b6-44c5-a589-ca4ae2b87e39` | `7a6a610279f8ae28ce5912512b235ca65a7501fbf3c258410849828b4361f380` | Pixel-identical; no drift. |
| Pro modal `1:971` | `https://www.figma.com/api/mcp/asset/b4d1153c-aa66-422b-a464-5b52f1417355` | `https://www.figma.com/api/mcp/asset/ec71e5cc-60cc-4501-b65b-59531af7d050` | `215dc56df3d2da0494609a857ecbb3125ab18c45741a0774810f9f630a053fcc` | Pixel-identical; no drift. |

No rollback was required.

## Intentionally left as-is

- Component contents, names, variant properties, component properties, and bindings were left unchanged by scope.
- Source-screen node trees were left unchanged because set-container resizing did not produce visual drift.
- Large component-set widths are intentional: the mandatory height-ratio rule requires variants to be shown in one row, and the surrounding specs/sections now hug those widths without overflow.

## Re-audit result

- Category/spec structure remains intact.
- All masters remain directly in their matching Canvas.
- All mandatory layout checks pass.
- No unpassed items remain in the authorized scope.

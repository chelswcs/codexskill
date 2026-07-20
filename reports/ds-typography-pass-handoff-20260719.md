# DS-skill-test typography consolidation handoff

Date: 2026-07-19  
Figma file: [DS-skill-test](https://www.figma.com/design/FkBEN1gq0fSMKe7y1Yor6D/DS-skill-test?node-id=0-1)  
Scope: local text styles and the Foundations Typography documentation only.

## Result

The approved typography consolidation is complete. The visible policy note in Foundations reads:

> Space Grotesk is used only for numerals and labels. Inter is used for body text and headings.

No source screen or component master was restyled in this pass. The final live inventory is **7 local text styles**, not 8: the file began with 10 styles and the three explicitly approved deletions leave 7. No unsupported eighth style was invented.

Final Typography section: [screenshot](https://www.figma.com/api/mcp/asset/1e7d20bd-4602-48de-a461-85d347d40389) (`4:69`, rendered 1200×1289 from 1120×1209).

## Final text styles and usage notes

| Text style | Usage note |
|---|---|
| Typography / Space Grotesk / Label 12 Medium | Compact labels, badges, and small control annotations only. |
| Typography / Space Grotesk / Numeric 14 Regular | Numeric values and compact numeric labels only. |
| Typography / Space Grotesk / Label 16 Medium | Uppercase navigation, action, and control labels only. |
| Typography / Space Grotesk / Label 18 Medium | Prominent numeric labels and selector values; not body copy or headings. |
| Typography / Space Grotesk / Metric 32 Medium | Large numeric metrics, rates, and financial values. |
| Typography / Space Grotesk / Display 64 Regular | Extra-large numeric display values only. |
| Typography / Inter / Body 14 Medium | The body/UI style for body copy, table content, supporting text, and metadata. |

The Figma API returned exactly these 7 local text styles. The documentation stack `4:112` contains the policy block plus 7 specimen frames.

## Renamed, repurposed, and deleted styles — in-context evidence

These are source-screen context captures, not specimen-only evidence. Nested text IDs identify the exact treatment; the screenshot target is the nearest normal source instance because screenshot rendering does not accept nested instance IDs containing semicolons.

| Decision | In-context source evidence | Context capture | Completed action |
|---|---|---|---|
| Rename Space Grotesk Body 16 Medium → Label 16 Medium | Header label “Pro Earn”, `I17:910;9:93`, Space Grotesk Medium 16 uppercase, within source instance `17:910` | [Header context](https://www.figma.com/api/mcp/asset/5f0a9ca6-f68c-4108-9d0c-c0c914f9cd0c) | Renamed and restricted to uppercase navigation/action/control labels. |
| Delete Inter Body 16 Medium | Raw Strategy Toggle label “Buy low”, `1:159`, Inter Medium 16 uppercase, within `1:155` | [Strategy Toggle context](https://www.figma.com/api/mcp/asset/b7c19903-ea59-4b18-9941-3a8424d370d5) | Deleted. Source text remains untouched for the later master-style migration pass. |
| Rename Space Grotesk Body 14 Regular → Numeric 14 Regular | Earn panel value “$67,000”, `I17:972;9:327;6:194`, Space Grotesk Regular 14, within `17:972` | [Earn panel context](https://www.figma.com/api/mcp/asset/4ee57463-e78c-480a-a3c8-953a569aef4e) | Renamed and limited to numeric values/compact numeric labels. |
| Keep Inter Body 14 Medium as THE body/UI style | Earn panel label “Deposit”, `I17:972;9:317;6:149`, Inter Medium 14, within `17:972` | [Earn panel context](https://www.figma.com/api/mcp/asset/4ee57463-e78c-480a-a3c8-953a569aef4e) | Kept; usage note now identifies it as the body/UI style. |
| Rename Space Grotesk Heading 32 Medium → Metric 32 Medium | Earn panel rate “22.31”, `I17:972;9:327;6:196`, Space Grotesk Medium 32, within `17:972` | [Earn panel context](https://www.figma.com/api/mcp/asset/4ee57463-e78c-480a-a3c8-953a569aef4e) | Repurposed for large numeric metrics, rates, and financial values. |
| Delete IBM Plex Mono Metric 32 Regular | Settlement panel “%”, `I17:1078;9:827`, IBM Plex Mono Regular 32, within `17:1078` | [Settlement panel context](https://www.figma.com/api/mcp/asset/604f995c-076c-427c-9077-492c3fddec25) | Deleted style and specimen. Existing IBM Plex Mono source text is intentionally untouched and is deferred to the master-style migration pass. |
| Delete Inter Heading 24 Bold | Logo placeholder “Prodigy.fi”, `I17:910;9:89`, Inter Bold 24 uppercase, within `17:910` | [Header context](https://www.figma.com/api/mcp/asset/5f0a9ca6-f68c-4108-9d0c-c0c914f9cd0c) | Deleted style and specimen. The logo remains a manual uppercase exception. |
| Rename Space Grotesk Title 18 Medium → Label 18 Medium | Results value “$ 1,950”, `I18:1037;9:1571;6:233`, Space Grotesk Medium 18, within `18:1037` | [Results table context](https://www.figma.com/api/mcp/asset/e297f28a-03c0-4bb1-b4f3-0cf6df1aedd1) | Renamed to keep Space Grotesk out of heading semantics and document its numeric-label role. |

## Deleted-style verification

The final local-style query returned none of these names:

- Typography / Inter / Body 16 Medium
- Typography / Inter / Heading 24 Bold
- Typography / IBM Plex Mono / Metric 32 Regular

Their former specimen nodes `4:134`, `4:137`, and `4:140` also no longer exist.

## Foundations layout verification

- Typography section: `4:69`, 1120×1209.
- Documentation frame: `4:70`, vertical auto-layout, hug height, clipping off.
- Specimen stack: `4:112`, vertical auto-layout, hug height, clipping off.
- Policy block: `30:935`, vertical auto-layout, hug height, clipping off.
- Seven remaining specimen frames use vertical auto-layout, hug height, and clipping off.
- Programmatic containment audit: **0 child nodes overflow their specimen parent**.
- Visual review of the final section found no clipping or overlap.

## Source-screen no-change verification

The pass made no write to any of the four source-screen nodes. A final programmatic traversal also found **0 references to any affected local text-style ID on every screen**, so renaming/deleting the local styles did not propagate into the screen text. Before and after captures have matching natural dimensions.

| Screen | Before capture | After capture | Natural size | Affected local-style refs | Result |
|---|---|---|---:|---:|---|
| Simple base `1:96` | [before](https://www.figma.com/api/mcp/asset/90e4cca9-5ba5-4f7e-9f06-c97e4e9e5f55) | [after](https://www.figma.com/api/mcp/asset/cd14366c-c093-42f9-8852-d42d37af7a82) | 1440×1400 | 0 | No source-screen change attributable to this pass. |
| Simple result `1:429` | [before](https://www.figma.com/api/mcp/asset/58afad11-ee2f-4750-b4f0-51d63216d0a5) | [after](https://www.figma.com/api/mcp/asset/332aa06d-5cf6-41ba-a118-15a6f876ae45) | 1440×1400 | 0 | No source-screen change attributable to this pass. |
| Pro base `1:781` | [before](https://www.figma.com/api/mcp/asset/b16986d3-1f6d-448e-93df-147d403f828a) | [after](https://www.figma.com/api/mcp/asset/dd416794-975d-49a3-92dc-f0a57fc77623) | 1440×1117 | 0 | No source-screen change attributable to this pass. |
| Pro result `1:971` | [before](https://www.figma.com/api/mcp/asset/706169e7-42b1-4318-be0e-5d2ebfbef0c4) | [after](https://www.figma.com/api/mcp/asset/a6afcecb-2c65-42c7-976d-f070bf4e8181) | 1440×1117 | 0 | No source-screen change attributable to this pass. |

Exact local PNG byte comparison could not be run because the workspace shell could not resolve `www.figma.com`; this limitation does not affect the Figma-side screenshot captures. The conclusion above is based on write scope, matching capture dimensions, visual capture review, and the zero-reference traversal rather than an unperformed pixel hash.

## Deferred work

- Apply the approved styles to component masters in a later pass, then validate instance propagation on the source screens.
- Migrate existing IBM Plex Mono source treatments during that master-style pass; none were altered here.
- Propose a genuine Inter 24px heading style only if future in-context evidence demonstrates a recurring heading need.

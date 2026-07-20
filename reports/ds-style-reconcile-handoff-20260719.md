# DS-skill-test style reconciliation handoff

Date: 2026-07-19  
Status: **BLOCKED — read-only inventory and baselines captured; no Figma writes performed**  
File: [DS-skill-test](https://www.figma.com/design/FkBEN1gq0fSMKe7y1Yor6D/DS-skill-test?node-id=0-1)

Retry note: after the user re-authorized the pass in chat, a fresh read-only `use_figma` identity check was attempted. The connector again returned `user cancelled MCP tool call` immediately. The Figma execution session therefore remains unavailable independently of chat-level write authorization.

Second retry note: after another explicit user authorization, the governing skills were reloaded and a new read-only file-identity check was issued. It again returned `user cancelled MCP tool call` before executing. Metadata/screenshots remain available, but reconciliation writes cannot run until the `use_figma` connector session itself is restored.

## Blocking condition

The Figma metadata, design-context, and screenshot tools work, but the general Figma execution surface required for exact node-reference inventory and all writes returns `user cancelled MCP tool call` immediately. This repeated for:

- a compact Components-page style inventory;
- a component-master list;
- a Deposit Input-only style query;
- a no-op availability check;
- a second minimal component query after the context scan.

The extraction/audit skill requires stopping on a Figma execution error rather than guessing or claiming writes. Consequently, **no style binding, style deletion, line-height change, or layout change was made**.

## Important feasibility finding

The seven `Typography/*` styles are local (`remote: false`). All 18 observed `Source/*` objects resolve as **remote styles** (`remote: true`, style IDs include a remote source suffix such as `,59:236`). Remote style objects cannot be deleted from this file through the local-style API. A successful continuation can remove every master reference to them; deletion must happen in their owning library/file, or “retire” must mean “zero references in DS-skill-test.”

## Complete style-object inventory captured before writes

### Local documented family

| Style | Font | Size | Line height | Case |
|---|---|---:|---|---|
| Typography/Space Grotesk/Label 12 Medium | Space Grotesk Medium | 12 | 100% | Original |
| Typography/Space Grotesk/Numeric 14 Regular | Space Grotesk Regular | 14 | 100% | Original |
| Typography/Space Grotesk/Label 16 Medium | Space Grotesk Medium | 16 | Auto | Upper |
| Typography/Space Grotesk/Label 18 Medium | Space Grotesk Medium | 18 | Auto | Original |
| Typography/Space Grotesk/Metric 32 Medium | Space Grotesk Medium | 32 | 100% | Original |
| Typography/Space Grotesk/Display 64 Regular | Space Grotesk Regular | 64 | 100% | Original |
| Typography/Inter/Body 14 Medium | Inter Medium | 14 | 100% | Original |

### Referenced remote Source family

| Style | Font | Size | Line height | Case |
|---|---|---:|---|---|
| Source/Space Grotesk/Medium/16 · Auto | Space Grotesk Medium | 16 | Auto | Original |
| Source/Inter/Semi Bold/18 · Auto · UPPER | Inter Semi Bold | 18 | Auto | Upper |
| Source/Inter/Semi Bold/16 · Auto | Inter Semi Bold | 16 | Auto | Original |
| Source/Inter/Medium/18 · 100% | Inter Medium | 18 | 100% | Original |
| Source/Inter/Medium/14 · 100% | Inter Medium | 14 | 100% | Original |
| Source/Inter/Medium/40 · 100% | Inter Medium | 40 | 100% | Original |
| Source/Inter/Regular/40 · 100% | Inter Regular | 40 | 100% | Original |
| Source/Inter/Medium/16 · Auto | Inter Medium | 16 | Auto | Original |
| Source/Space Grotesk/Regular/10 · Auto | Space Grotesk Regular | 10 | Auto | Original |
| Source/Inter/Semi Bold/16 · Auto · UPPER | Inter Semi Bold | 16 | Auto | Upper |
| Source/Inter/Medium/16 · Auto · UPPER | Inter Medium | 16 | Auto | Upper |
| Source/Space Grotesk/Regular/14 · 100% | Space Grotesk Regular | 14 | 100% | Original |
| Source/Space Grotesk/Medium/32 · 100% | Space Grotesk Medium | 32 | 100% | Original |
| Source/Space Grotesk/Medium/12 · 100% | Space Grotesk Medium | 12 | 100% | Original |
| Source/Inter/Regular/12 · 100% | Inter Regular | 12 | 100% | Original |
| Source/Inter/Bold/24 · Auto · UPPER | Inter Bold | 24 | Auto | Upper |
| Source/Space Grotesk/Bold/16 · Auto · UPPER | Space Grotesk Bold | 16 | Auto | Upper |
| Source/Space Grotesk/Medium/16 · Auto · UPPER | Space Grotesk Medium | 16 | Auto | Upper |

No third style family was returned by the style-object resolution. Raw, unstyled master text does exist and still requires the exact per-node execution inventory.

## Verified master usage found before the block

The Components scan found 281 text nodes inside component-master subtrees and resolved the 18 Source styles above. The connector truncated the first full node dump, so this is not presented as the required complete per-node map.

Exact examples verified through design context:

| Component | Text node(s) | Current treatment |
|---|---|---|
| Button / Connect Wallet `6:28` | `6:27` “Connect wallet” | Source/Space Grotesk/Medium/16 · Auto |
| Deposit Input / Wide `6:156` | `6:149` “Deposit” | Source/Inter/Medium/14 · 100% |
| Deposit Input / Wide `6:156` | `6:151` “0.05” | Source/Inter/Medium/40 · 100% |
| Deposit Input / Wide `6:156` | `6:152` “BTC” | Source/Inter/Regular/40 · 100% |
| Deposit Input / Wide `6:156` | `6:154` “MAX” | Source/Inter/Medium/14 · 100% |
| Deposit Input / Compact `6:165` | `6:158`, `6:160`, `6:161`, `6:163` | Same four treatments as Wide |
| Deposit Input / Modal `6:174` | `6:167`, `6:169`, `6:170`, `6:172` | Same four treatments as Wide |
| Strategy Toggle variants | `7:102`, `17:575` “Buy low” | Inter Medium 16, Auto, uppercase Source treatment |
| Raw Result Row masters | `6:236`, `6:245` “1,566 %” | Raw Space Grotesk Medium 18 |

The required complete mapping for all 281 component-master text nodes and all 67 Foundations text nodes remains pending because only `use_figma` exposes exact text-style IDs and raw segment data reliably.

## Preliminary exact-match rebind candidates

These are candidates only; none was applied:

| Current Source style | Documented target | Match assessment |
|---|---|---|
| Source/Space Grotesk/Regular/14 · 100% | Typography/Space Grotesk/Numeric 14 Regular | Exact font, weight, size, line height, case |
| Source/Space Grotesk/Medium/32 · 100% | Typography/Space Grotesk/Metric 32 Medium | Exact |
| Source/Space Grotesk/Medium/12 · 100% | Typography/Space Grotesk/Label 12 Medium | Exact |
| Source/Space Grotesk/Medium/16 · Auto · UPPER | Typography/Space Grotesk/Label 16 Medium | Exact |
| Source/Inter/Medium/14 · 100% | Typography/Inter/Body 14 Medium | Exact |

Each individual node still requires a before/after master screenshot comparison before its binding can be accepted.

## Scale-gap proposals — not created

These preliminary gaps are evidenced by production masters. The exact affected-node list and in-context crops must be completed after the execution surface resumes.

| Actual need | Known evidence | Proposed style | Fixed options |
|---|---|---|---|
| 40px numeric value, Medium | Deposit values `6:151`, `6:160`, `6:169` | Typography / Space Grotesk / Numeric 40 Medium | adopt proposed style / map to nearest existing / leave raw with reason |
| 40px numeric/unit value, Regular | Deposit units `6:152`, `6:161`, `6:170` | Typography / Space Grotesk / Numeric 40 Regular | adopt proposed style / map to nearest existing / leave raw with reason |
| 10px compact numeric/label | Expiry Selector uses Source/Space Grotesk/Regular/10 · Auto | Typography / Space Grotesk / Label 10 Regular | adopt proposed style / map to nearest existing / leave raw with reason |
| 12px supporting label, Regular | APY Tile uses Source/Inter/Regular/12 · 100% | Typography / Inter / Body 12 Regular | adopt proposed style / map to nearest existing / leave raw with reason |
| 16px original-case label | Connect Wallet and other Source/Space Grotesk/Medium/16 · Auto nodes | Typography / Space Grotesk / Label 16 Medium (original-case variant or documented exception) | adopt proposed style / map to nearest existing / leave raw with reason |
| 16px bold uppercase label | Navigation uses Source/Space Grotesk/Bold/16 · Auto · UPPER | Typography / Space Grotesk / Label 16 Bold | adopt proposed style / map to nearest existing / leave raw with reason |
| 18px action label | Buttons use Inter Semi Bold 18 uppercase, conflicting with the Space-Grotesk-for-labels policy | Typography / Space Grotesk / Label 18 Semi Bold | adopt proposed style / map to nearest existing / leave raw with reason |
| 16px asset/control labels | Several masters use Inter Semi Bold/Medium 16 Source styles | Typography / Space Grotesk / Label 16 with confirmed weight/case | adopt proposed style / map to nearest existing / leave raw with reason |

No style was invented and no gap node was changed.

## Line-height decision status

No normalization was attempted. Label 16 and Label 18 remain Auto while the other documented styles remain 100%. Normalizing Auto to 100% can change glyph boxes and auto-layout; the required trial, master screenshots, and rollback cannot be performed without `use_figma`.

## Font Policy block status

`Font Policy` block `30:935` remains 1040px wide inside Type Specimens `4:112` at 960px. It was not changed because the write surface was unavailable.

## Before baselines captured

All 24 component masters were captured before any intended mutation:

| Master | Before screenshot |
|---|---|
| `6:28` | https://www.figma.com/api/mcp/asset/bc3b3407-9c94-41fb-b07f-db92c8ef08d9 |
| `6:31` | https://www.figma.com/api/mcp/asset/9e1c065f-4564-44eb-9c18-e553dd297c44 |
| `6:34` | https://www.figma.com/api/mcp/asset/0755e5b8-0d0d-4864-b5be-8d5339f251d9 |
| `6:40` | https://www.figma.com/api/mcp/asset/df15a8c6-e50b-490c-9813-9fa747b0a0f8 |
| `6:70` | https://www.figma.com/api/mcp/asset/53625174-5375-4823-be7e-c367217c1279 |
| `6:94` | https://www.figma.com/api/mcp/asset/e4c82346-1628-4def-afd6-bb91da630a78 |
| `6:120` | https://www.figma.com/api/mcp/asset/e776f65e-5691-45a3-9806-459e0edca9ce |
| `6:156` | https://www.figma.com/api/mcp/asset/9bd41ee4-6e23-4eb2-8f42-22a8fddb8a1e |
| `6:165` | https://www.figma.com/api/mcp/asset/b396bb51-91ff-4939-b194-935d47e061ed |
| `6:174` | https://www.figma.com/api/mcp/asset/95500fb2-47ae-4a56-a448-a7f42c490c59 |
| `7:83` | https://www.figma.com/api/mcp/asset/51157974-aa39-4078-87dd-46e27131a007 |
| `7:103` | https://www.figma.com/api/mcp/asset/aecd147d-acf0-426b-9ca1-6db4e03140d2 |
| `17:571` | https://www.figma.com/api/mcp/asset/da1f0bd7-6961-49c0-8a1d-66edf1b27a7a |
| `6:200` | https://www.figma.com/api/mcp/asset/bf1d2a6f-5596-417e-b211-ad00aaaae469 |
| `6:209` | https://www.figma.com/api/mcp/asset/0f49e359-1207-4930-b747-6bdcdcdc6ba6 |
| `6:231` | https://www.figma.com/api/mcp/asset/e2a9a6b4-1e2f-4d27-bd57-7662f80afe5b |
| `6:240` | https://www.figma.com/api/mcp/asset/8093f072-e510-44a7-8ad5-feeb2f524444 |
| `9:1652` | https://www.figma.com/api/mcp/asset/56325cfe-4eac-421e-93ae-07da6cf7a469 |
| `9:131` | https://www.figma.com/api/mcp/asset/b0a34f34-c0ae-4d35-9237-449006d4d46f |
| `10:671` | https://www.figma.com/api/mcp/asset/91bf74e3-8a84-48c6-a0b6-868f92ea8da5 |
| `9:416` | https://www.figma.com/api/mcp/asset/7a2e5f11-23c0-41fb-8557-af6e479cbb20 |
| `9:525` | https://www.figma.com/api/mcp/asset/024ce00e-bfb0-48e7-913b-752b31e30d73 |
| `9:961` | https://www.figma.com/api/mcp/asset/fe2cabfe-4a84-4e29-87c5-62aa7f1f3374 |
| `9:1124` | https://www.figma.com/api/mcp/asset/396fe382-95d5-48e7-80ac-e9e6c5b7bcad |

Source-screen baselines:

| Screen | Before screenshot | Natural size |
|---|---|---:|
| Simple base `1:96` | https://www.figma.com/api/mcp/asset/309f3999-3b65-4bb8-a3ba-d23ca1fe9b7d | 1440×1400 |
| Simple result `1:429` | https://www.figma.com/api/mcp/asset/1bbac91d-bf7e-4988-a324-53dbbd0248d1 | 1440×1400 |
| Pro base `1:781` | https://www.figma.com/api/mcp/asset/4baca438-5e1f-46d1-8cdc-3b0c05530c91 | 1440×1117 |
| Pro result `1:971` | https://www.figma.com/api/mcp/asset/fb449a4d-1d91-4622-9623-e82fe3b9ecb8 | 1440×1117 |

## Required continuation

1. Restore/approve the `use_figma` execution session.
2. Rerun the compact per-node segment inventory on Foundations and Components.
3. Apply only exact matches in small batches.
4. Capture every master after each batch and roll back any rendered drift.
5. Recount remaining Source references; do not claim remote object deletion from this file.
6. Trial line-height normalization one style at a time with rollback on drift.
7. Resize `30:935` to the 960px specimen-stack width.
8. Capture and compare all four source screens.
9. Replace this blocked handoff with the completed before/after inventory and results.

---

# 續完記錄（Claude 直接執行，2026-07-19）

Codex 的 use_figma 連線持續失效後，改由 Claude 端的 Figma 連線（c@ctrlspace.xyz）執行，範圍同原授權。

## 已完成

- 精確匹配 rebind：35 個 Source 樣式節點 + 14 個 raw 節點 → 文件 Typography/* 樣式，共 49 個 master 文字節點，全部零尺寸漂移、零失敗（逐節點驗證寬高變化 < 0.5px）
- Font Policy 區塊溢出修正：30:935 由 1040px 改為 FILL（960px），已截圖確認
- Simple base 畫面截圖抽查：與修復前一致，無漂移

## 目前狀態（master 文字節點，不含 instance 內部）

- 已綁文件樣式：49
- 仍在 Source/*：46（13 種樣式，全部因字家/字重/大小寫與 policy 衝突而需使用者決定）
- 仍為 raw：103（多數同樣涉及視覺變化決策）

## 待使用者決定（見決策頁 round-2）

A. 40px 輸入數值（Inter→SG?）／B. 18px 按鈕標籤／C. 16px 標籤家族統一／D. 12px/10px 輔助字／E. Settlement 雜項含 Mono 退役執行

## 備註

- Source/* 為遠端樣式（remote: true），本檔案內只能解除引用，刪除需至源頭 library
- 行高統一（Label 16/18 的 Auto → 100%）尚未執行，待缺口決策一併處理

---

# A–E 決策執行完成（Claude 執行，2026-07-19 清晨）

使用者決定：A 輸入維持 Inter／B 按鈕標籤維持 Inter／C 導覽標籤 SG、body 性質改 Inter、數字 SG／D 照建議且表頭併入 Label 12、10px 獨立／E 照建議全做（含 Mono 退役）。

## 執行結果（全部可對照檔案驗證）

- 新建 19 個本地樣式（Inter 例外組 + SG 數字標籤組），每個都有 usage note，例外樣式明確標註 EXCEPTION
- 綁定節點：73（無視覺變化）+ 66（授權視覺變更）+ 18（修正批），前兩輪 49 個合計約 196 個 master 文字節點已綁文件樣式
- **Source/* 遠端樣式引用：0**（目標達成；樣式本體屬外部 library，需至源頭刪除）
- **Raw 節點：2**（logo「Prodigy.fi」×2，依使用者決定維持手動格式的刻意例外）
- 本地樣式總數 26，全部展示於 Foundations Typography 區（含新示範 19 列，零溢出）
- Mono 已從元件完全退役；Settlement 面板截圖驗證版面無破損
- Result Row 高度維持 60 不變；USD 單位行高 22→18、Funds available 17→14 為預期的行高統一
- 12px 大寫表頭以「字元改大寫後綁 Label 12」處理（避免 textCase 覆寫打斷樣式連結的 Figma 行為）
- 「OR」字級 21.78 → 綁 Label 20 Medium

## 學到的 API 陷阱

綁定樣式後再設 textCase 等文字屬性會靜默解除樣式連結——需要大小寫差異時，改字元內容而不是設覆寫。

## 遺留事項

- Codex 端 use_figma 在 exec 模式被 PermissionRequest hook 自動取消（互動模式可解），本輪由 Claude 端連線執行
- Source/* 樣式本體仍在外部 library，如需清除要在源頭檔案操作

---

# 16px attribute-identical style merge completion（Codex，2026-07-20）

## Scope completed

The three user-approved, attribute-identical 16px pairs were merged across all three pages. Every matched text node was rebound with `setTextStyleIdAsync`; every node retained exactly the same width and height.

| Surviving style | Deleted style | Page 1 | Foundations | Components | Total rebound | Geometry drift |
|---|---|---:|---:|---:|---:|---:|
| `Typography/Space Grotesk/Label 16 Medium` | `Typography/Space Grotesk/Numeric 16 Medium` | 7 | 1 | 13 | **21** | 0 nodes |
| `Typography/Inter/Title 16 Semi Bold` | `Typography/Inter/Label 16 Semi Bold` | 2 | 1 | 2 | **5** | 0 nodes |
| `Typography/Inter/Body 16 Medium` | `Typography/Inter/Label 16 Medium` | 2 | 1 | 8 | **11** | 0 nodes |
| **Total** |  | **11** | **3** | **23** | **37** | **0 nodes** |

## Per-node geometry record

Each value is `before width×height → after width×height`.

### Numeric 16 Medium → Label 16 Medium

| Page | Text node | Geometry |
|---|---|---|
| Page 1 | `I17:942;6:67` | 84×20 → 84×20 |
| Page 1 | `I17:1078;9:846` | 53×20 → 53×20 |
| Page 1 | `I11:941;6:67` | 84×20 → 84×20 |
| Page 1 | `I11:1322;9:1009` | 53×20 → 53×20 |
| Page 1 | `I18:1009;6:91` | 84×20 → 84×20 |
| Page 1 | `I11:1978;6:91` | 84×20 → 84×20 |
| Page 1 | `I11:2244;6:117` | 84×20 → 84×20 |
| Foundations | `42:957` | 84×20 → 84×20 |
| Components | `6:67` | 84×20 → 84×20 |
| Components | `6:91` | 84×20 → 84×20 |
| Components | `6:117` | 84×20 → 84×20 |
| Components | `9:829` | 65×20 → 65×20 |
| Components | `9:835` | 65×20 → 65×20 |
| Components | `9:841` | 65×20 → 65×20 |
| Components | `9:846` | 53×20 → 53×20 |
| Components | `9:942` | 85×20 → 85×20 |
| Components | `9:992` | 65×20 → 65×20 |
| Components | `9:998` | 65×20 → 65×20 |
| Components | `9:1004` | 65×20 → 65×20 |
| Components | `9:1009` | 53×20 → 53×20 |
| Components | `9:1105` | 85×20 → 85×20 |

### Label 16 Semi Bold → Title 16 Semi Bold

| Page | Text node | Geometry |
|---|---|---|
| Page 1 | `I18:1032;17:573` | 83×19 → 83×19 |
| Page 1 | `I11:2006;7:100` | 83×19 → 83×19 |
| Foundations | `42:1002` | 83×19 → 83×19 |
| Components | `7:100` | 83×19 → 83×19 |
| Components | `17:573` | 83×19 → 83×19 |

### Label 16 Medium → Body 16 Medium

| Page | Text node | Geometry |
|---|---|---|
| Page 1 | `I18:1032;17:575` | 74×19 → 74×19 |
| Page 1 | `I11:2006;7:102` | 74×19 → 74×19 |
| Foundations | `42:997` | 74×19 → 74×19 |
| Components | `7:102` | 74×19 → 74×19 |
| Components | `17:575` | 74×19 → 74×19 |
| Components | `9:236` | 66×19 → 66×19 |
| Components | `9:242` | 66×19 → 66×19 |
| Components | `9:248` | 66×19 → 66×19 |
| Components | `9:442` | 66×19 → 66×19 |
| Components | `9:448` | 66×19 → 66×19 |
| Components | `9:454` | 66×19 → 66×19 |

## Styles and Foundations cleanup

- Deleted local styles:
  - `Typography/Space Grotesk/Numeric 16 Medium` — `S:9df39d2a0cdf8e3e4a9e556ce21cf60d814576f8,`
  - `Typography/Inter/Label 16 Semi Bold` — `S:0fe015a4f3bfceac43b4c96660d058c0834ce25c,`
  - `Typography/Inter/Label 16 Medium` — `S:b034acef97311e3035053a5ecb1094a665fe73b2,`
- Removed deprecated specimen frames `42:955`, `42:1000`, and `42:995`.
- Updated surviving usage notes:
  - `16:1260`: “CAPTION + DATA VALUE — navigation/action/control labels and 16px numeric values.”
  - `42:994`: “TITLE + CONTROL LABEL — asset-pair titles and 16px semi-bold uppercase active control labels.”
  - `42:989`: “BODY + CONTROL/DATA LABEL — body-nature 16px text, medium-weight control labels, and 16px data labels.”
- Typography stack `4:112`: 22 children = Font Policy + 21 specimens; 960×2651.
- Documentation `4:70`: 1040×2794 at (40,70).
- Typography section `4:69`: resized to 1120×2934; documentation containment check passed.

## Final local text-style order

Final count: **21**. Styles are ordered per family folder, then size descending and weight descending:

1. Typography/Space Grotesk/Numeric 40 Medium
2. Typography/Space Grotesk/Metric 32 Medium
3. Typography/Space Grotesk/Label 20 Bold
4. Typography/Space Grotesk/Label 20 Medium
5. Typography/Space Grotesk/Numeric 18 Medium
6. Typography/Space Grotesk/Label 16 Bold
7. Typography/Space Grotesk/Label 16 Medium
8. Typography/Space Grotesk/Label 14 Bold
9. Typography/Space Grotesk/Label 14 Medium
10. Typography/Space Grotesk/Numeric 14 Medium
11. Typography/Space Grotesk/Numeric 14 Regular
12. Typography/Space Grotesk/Label 12 Medium
13. Typography/Space Grotesk/Label 10 Regular
14. Typography/Inter/Input 40 Medium
15. Typography/Inter/Input 40 Regular
16. Typography/Inter/Label 18 Semi Bold
17. Typography/Inter/Body 18 Medium
18. Typography/Inter/Title 16 Semi Bold
19. Typography/Inter/Body 16 Medium
20. Typography/Inter/Body 14 Medium
21. Typography/Inter/Body 12 Regular

## Verification

- Deprecated-style references after deletion: Page 1 = 0, Foundations = 0, Components = 0.
- Deleted style names present in the final local-style inventory: 0.
- Geometry drift across all 37 rebound text nodes: 0.
- [Final Typography screenshot](https://www.figma.com/api/mcp/asset/38fd356b-fabc-4027-a8c2-7b18e56afbcf), node `4:69`, natural size 1120×2934.
- Source screen `1:96`: [before](https://www.figma.com/api/mcp/asset/7c420e72-1cac-47c1-90e8-a52864ceaef4) / [after](https://www.figma.com/api/mcp/asset/d756581e-2e8b-43b8-9704-3f07b719d914), both 1440×1400.
- Before and after `1:96` PNG SHA-256: `9b046212545e90d896ee3a6d851e6d9f2208629a2590d0686b9156501b710fe8`; byte comparison exit code 0. The screen is pixel-identical.

---

# Role-based taxonomy reorganization completion（Codex，2026-07-20）

## Scope completed

- Reorganized all local text styles from font-family folders into the approved role folders: `Heading`, `Title`, `Body`, `Numeric`, `Nav`, `Action`, `Input`, `Label`.
- Renamed all 21 pre-existing local styles without changing their typography attributes.
- Created one style, `Typography/Numeric/16 Medium` (`S:ba12c448f1ab083b4e43f4f846b8630d242803af,`): Space Grotesk Medium, 16px, Auto line height, 0% letter spacing, Original case.
- Rebound numeric/currency text formerly sharing `Typography/Nav/16 Medium` to the new Numeric style on Components and Page 1.
- Updated all 22 style descriptions, specimen frame names, visible Style Name labels, and visible usage notes.
- Added the Numeric/16 Medium specimen `58:936` and sorted the documentation and style panel into the same role order.

## Final local text styles and usage notes

The following is the final `getLocalTextStylesAsync()` order; it matches the Type Specimens order under `4:112`.

| # | Style | Usage note / style description |
|---:|---|---|
| 1 | `Typography/Heading/20 Bold` | HEADING — 20px emphasized settlement state headings (BELOW/ABOVE); type characters in uppercase. |
| 2 | `Typography/Heading/20 Medium` | HEADING — 20px settlement target headings; type characters in uppercase. |
| 3 | `Typography/Heading/14 Medium` | HEADING — 14px chart annotations and table headings; type characters in uppercase. |
| 4 | `Typography/Title/16 Semi Bold` | TITLE — 16px asset-pair titles and semi-bold active control titles. |
| 5 | `Typography/Body/18 Medium` | BODY — 18px unit and vault text (USD, USDC, vault names). |
| 6 | `Typography/Body/16 Medium` | BODY — 16px body copy and medium-weight UI text. |
| 7 | `Typography/Body/14 Medium` | BODY — primary body/UI style for body copy, table content, supporting text, and metadata. |
| 8 | `Typography/Body/12 Regular` | BODY — 12px supporting text such as APY annotations. |
| 9 | `Typography/Numeric/40 Medium` | DATA VALUE — large 40px numeric values outside inputs (settlement receive amounts). |
| 10 | `Typography/Numeric/32 Medium` | DATA VALUE — large numeric metrics, rates, and financial values. |
| 11 | `Typography/Numeric/18 Medium` | DATA VALUE — 18px numeric values (result-row amounts and selector values). |
| 12 | `Typography/Numeric/16 Bold` | DATA VALUE — bold 16px numeric emphasis such as balances and chart endpoints. |
| 13 | `Typography/Numeric/16 Medium` | DATA VALUE — 16px numeric values such as prices and chart figures. |
| 14 | `Typography/Numeric/14 Bold` | DATA VALUE — bold 14px numeric delta callouts such as 0.05% BELOW. |
| 15 | `Typography/Numeric/14 Medium` | DATA VALUE — medium-weight 14px numeric values and dates. |
| 16 | `Typography/Numeric/14 Regular` | DATA VALUE — 14px numeric values and compact numeric labels. |
| 17 | `Typography/Nav/16 Medium` | NAV (EXCEPTION: Space Grotesk) — 16px navigation titles such as SIMPLE EARN, PRO EARN, PORTFOLIO, STRATEGY VAULTS, MORE, and EN. |
| 18 | `Typography/Action/18 Semi Bold` | ACTION (EXCEPTION) — 18px button and CTA labels; Inter is retained per user decision. |
| 19 | `Typography/Input/40 Medium` | INPUT (EXCEPTION) — 40px deposit input values; Inter is retained per user decision. |
| 20 | `Typography/Input/40 Regular` | INPUT (EXCEPTION) — 40px deposit input currency units; Inter is retained per user decision. |
| 21 | `Typography/Label/12 Medium` | CAPTION — compact annotations, badges, and small control labels; type characters in uppercase. |
| 22 | `Typography/Label/10 Regular` | CAPTION — tiny supporting annotations such as expiry countdowns; type characters in uppercase. |

Final local text-style count: **22**.

## Numeric/Nav split and drift record

All entries below retained the same width and height after `setTextStyleIdAsync`.

### Components — 13 nodes rebound

| Text node | Content | Before → after |
|---|---|---|
| `6:67` | `$64,139.69` | 84×20 → 84×20 |
| `6:91` | `$64,139.69` | 84×20 → 84×20 |
| `6:117` | `$64,139.69` | 84×20 → 84×20 |
| `9:829` | `$59,000` | 65×20 → 65×20 |
| `9:835` | `$59,000` | 65×20 → 65×20 |
| `9:841` | `$59,000` | 65×20 → 65×20 |
| `9:846` | `59,700` | 53×20 → 53×20 |
| `9:942` | `59,000` | 85×20 → 85×20 |
| `9:992` | `$59,000` | 65×20 → 65×20 |
| `9:998` | `$59,000` | 65×20 → 65×20 |
| `9:1004` | `$59,000` | 65×20 → 65×20 |
| `9:1009` | `59,700` | 53×20 → 53×20 |
| `9:1105` | `59,000` | 85×20 → 85×20 |

### Page 1 — 7 nodes rebound

| Text node | Content | Before → after |
|---|---|---|
| `I17:942;6:67` | `$64,139.69` | 84×20 → 84×20 |
| `I17:1078;9:846` | `59,700` | 53×20 → 53×20 |
| `I11:941;6:67` | `$64,139.69` | 84×20 → 84×20 |
| `I11:1322;9:1009` | `59,700` | 53×20 → 53×20 |
| `I18:1009;6:91` | `$64,139.69` | 84×20 → 84×20 |
| `I11:1978;6:91` | `$64,139.69` | 84×20 → 84×20 |
| `I11:2244;6:117` | `$64,139.69` | 84×20 → 84×20 |

Geometry drift: **0 of 20 rebound nodes**. Foundations had no numeric text on the former shared style; its existing `SELL HIGH` specimen remained on Nav/16 Medium. The new Numeric specimen text is node `58:938` (`$64,139.69`, 84×20).

## Foundations documentation result

| Node | Before | After |
|---|---:|---:|
| Type Specimens `4:112` | 960×2651, Font Policy + 21 specimens | 960×2772, Font Policy + 22 specimens |
| Documentation `4:70` | 1040×2794 | 1040×2915 |
| Typography section `4:69` | 1120×2934 | 1120×3055 |

- All specimen frames follow `Specimen / Typography/<Role>/<Size Weight>`.
- Every visible Style Name text exactly matches its local style name.
- Specimen order is folder order `Heading → Title → Body → Numeric → Nav → Action → Input → Label`, with size descending and weight descending within a role.
- [Final Typography screenshot](https://www.figma.com/api/mcp/asset/5960abf4-d277-4395-95c9-9ce39dcb2bc7), node `4:69`, natural size 1120×3055.

## Verification

| Check | Foundations | Components | Page 1 |
|---|---:|---:|---:|
| Broken text-style references | 0 | 0 | 0 |
| Numeric-containing text still on `Typography/Nav/16 Medium` | 0 | 0 | 0 |
| Text on new `Typography/Numeric/16 Medium` | 1 specimen | 13 nodes | 7 nodes |

- `getLocalTextStylesAsync()` returned 22 styles in the exact order listed above; Type Specimens returned the same order.
- Screen `1:96`: [before capture](https://www.figma.com/api/mcp/asset/3ff04e49-5b28-488d-bd68-5c5f54684ca7) / [after capture](https://www.figma.com/api/mcp/asset/a2bc9917-89cb-49e4-b71c-ba0715448a54), both 1440×1400.
- Final `1:96` PNG SHA-256: `9b046212545e90d896ee3a6d851e6d9f2208629a2590d0686b9156501b710fe8`, identical to the established pre-pass screen baseline recorded in the preceding completion section. The screen is pixel-identical.

# Handoff: continue Petal's Adventures in Claude Cowork

**Why:** Higgsfield's trial unlimited generations do not work from Claude Code ("available in: Claude chat, Claude Cowork, ChatGPT"). The trial (`mcp_ultra_unlim`) is active until **2026-11-17 19:48 UTC**. Run all generation from Cowork with the Higgsfield connector, and pass `use_unlim: true` on every generate call.

## Where we are
- ✅ P0–P2: visual traits, series bible, and 5 scripts (v3). **Gate 1 approved.**
- ✅ P3: Style Bible at `production/art/style_bible.md`.
- ✅ P4 (Petal only): turnaround v2 + expression sheet v2. **Gate 2 pending user approval.**
- ⏭ Next: the other 5 characters (Biscuit, Sultana, Captain Karak, Noor, Mochi) + Jamal and props → environments → key frames → Seedance 2.5 shots → sound → edit → delivery.

## Files to load into Cowork (from repo branch `claude/petals-adventures-video-series-j5297b`)
- `PETALS_ADVENTURES_MASTER_PROMPT.md`: the full pipeline (graph, loops, crew, rubrics)
- `production/story/`: `petal_visual_traits.md`, `series_bible.md`, `ep01–05_script.md`
- `production/review/p2_final_social_kit.md`: captions and hashtags
- `production/art/style_bible.md`
- `production/assets/registry.json`: Higgsfield media and job IDs
- `production/log.md` + `production/state.json`: decisions and resume point

## Reusable Higgsfield IDs (same account; reusable as `medias[].value`)
| Asset | ID |
|---|---|
| Petal turnaround v2 (approved candidate) | `f3ec5ede-e6ef-4dcc-9b67-efa3b4273af1` |
| Petal expressions v2 | `62b0c2dd-448c-460f-8438-2e361939784b` |
| Photo: sitting front | `19d5fc6f-8239-46ed-ada9-7111b3a11465` |
| Photo: side profile + harness | `aa0353cf-1186-4602-b7a2-e088d61b5869` |
| Photo: side, spots/patch | `8b72810d-09bb-41d7-a1c3-3c790fba70fa` |
| Photo: face close-up | `f2bda34b-b2aa-4373-b79a-2234f4807170` |
| Photo: happy front | `56812ff0-8842-4e5f-a93f-5d4d0d6bc6c3` |
| Photo: walking 3/4 | `42638091-6b2b-4772-ac5f-2d39b5df83b3` |

## Paste this into Cowork to resume
> You are the Showrunner of "Petal's Adventures". Read PETALS_ADVENTURES_MASTER_PROMPT.md and production/HANDOFF_COWORK.md, then resume from Gate 2. Gate 1 is approved. Use the Higgsfield connector with `use_unlim: true` on every generation (nano_banana_pro for images, seedance_2_5 for video). Reuse the IDs in the handoff table. Before continuing, fix two things on Petal's expression sheet (job 62b0c2dd…): soften the eye haze slightly, and make both eyes match in the DETERMINED panel. Then show me Petal's sheets for Gate 2 approval, and after that run P4 → P9 autonomously.

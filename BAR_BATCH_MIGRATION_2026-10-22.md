# Bar Batch Migration — 2026-10-22

## Scope

- Bar clips in `ok_5files_all`: 153
- Human-reviewed and approved: `bar_1`–`bar_34`
- Automatically migrated and pending human review: `bar_35`–`bar_163` (119 clips)
- Hardcase flags: 63 clips total (including `bar_28`)

## What changed

For every remaining bar clip:

- normalized the input table and removed sidecar-only columns;
- retained the existing intent as a pending-review draft;
- migrated legacy G1 units into the current `requirements + units` R/U schema;
- added `g0_data_completeness` for static or state-sequence bar coverage;
- removed legacy `g1_draft_b2.json` and `g2_evidence.json` from the dataset;
- copied the updated files into both dataset layouts;
- recorded status and hardcase flags in `BAR_REVIEW_INDEX.csv`.

## Automatic hardcase types

- `legacy_units_without_visual_basis`
- `no_explicit_bar_mark_in_reference_svg`

## Review caveats

- `bar_35` onward are conservative automated migrations, not final semantic approvals.
- All intents from the legacy corpus still require semantic review.
- `no_explicit_bar_mark_found` means the reference SVG does not contain a recognizable
  `data-role="bar"` mark; some may use custom graphics and need visual inspection.
- G1 units that depended only on narration or had no basis were set to
  `must_be_visualized=false` and flagged as hardcases.
- `legacy_unit_count_above_4` is present for two complex clips and should be reviewed first.

## Validation

- Every bar clip has `data_table.csv`, `intent.json`, `g1.json`, `chart_spec.json`,
  `input_spec.json`, `narration.jsonl`, `semantic.svg`, and `keyframe.png`.
- All JSON files parse.
- `check_bar_completeness.py`: `checked=153 failures=0`.

## Main review file

Use `BAR_REVIEW_INDEX.csv` at the dataset repository root. Filter on:

- `status=agent_draft_pending_human_review`
- `hardcase=True`
- `review_flags` containing `no_explicit_bar_mark_found` or `legacy_unit_count_above_4`

# G1 Hardcases

## Definition

A required semantic unit is a **hardcase** when both of the following hold:

1. The proposition is necessary to complete the public intent and is supported
   by the public V1 inputs (`intent_en`, `data_table.csv`, `chart_spec.json`).
2. The source chart has no obvious direct data mark, axis, label, or other
   visual encoding for that proposition.

This is different from an unsupported narration claim. If a claim is only in
the source narration and is not supported by the table or intent, it remains
`optional_valid` or unsupported; it does not become a hardcase G1 unit.

## Default handling

- Keep the hardcase in G1 if deleting it would make the intent incomplete.
- Set `must_be_visualized=false` by default.
- Its `C_u` score still enters `ContentCompletion`.
- It is excluded from `VisualCompletion` and `JointCompletion` denominators
  unless the task explicitly asks every required unit to be visualized.
- Accept flexible generated visualizations when present, such as a readable
  annotation or callout tied to the relevant evidence. Do not prescribe one
  fixed icon or layout.
- Record a `hardcase` flag and a short `hardcase_reason` in the G1 unit.

## Examples

### bar_22 / U3

- Claim: extreme ultra-rich wealth concentration is the rationale for a wealth
  tax that could fund programs benefiting millions.
- Public support: intent plus the contrast between named occupations and the
  off-scale ultra-rich tail.
- Source visual: no direct tax mark.
- Handling: `unit_kind=narrative_claim`, `must_be_visualized=false`.
- The independent V1 output additionally drew an off-scale ultra-rich arrow and
  a wealth-tax callout. This is accepted as a valid optional visual route, not
  as a requirement inherited from the source video.

### bar_28 / whole clip

- Type: `threshold_diagram_with_narration_only_claims`.
- The source visual is a wealth-threshold schematic, not a standard category bar
  chart. One illustrative wealth column crosses `$60M` and `$1B`; `2%` and `3%`
  are rate annotations attached to those thresholds.
- U1 (threshold-to-rate relationship) requires visual evidence.
- U2 (`0.05%` tax base) and U3 (`$200B` potential revenue) exist only in
  narration and use `must_be_visualized=false`.

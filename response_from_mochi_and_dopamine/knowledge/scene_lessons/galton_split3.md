# galton_split3 — REAL falling balls: 9 rows, 1 ball → 512 (batch71)

- Brief: docs/BRIEF_batch71.md §5 (owner: balls too small, no feeling of FALLING). New file `scenes/galton_split3.py` (from galton_split2; untouched).
- 9 rows (10 bins, S 38 px), every ball drawn (r 5.4 px). Row count: the centre bin must hold C(n, n/2) balls under ~480 px → 9 rows (126 balls, 3 per layer) keeps balls 11 px wide; 10 rows would need 8 px balls, 12 rows (brief's example, 4,096) 4 px.
- Motion: every hop peg→peg is a real parabola under the tilted board's gravity (G_B 691 px/s², 13 px bounce, 0.60 s per hop). Bolt's ball splits at every peg; the two children leave up to SPLIT_J 35 ms apart (so the 2^k balls read as a cascade, not one dot); his bins end at exactly C(9, j). Mochi: R 32.7 single balls/s since −3 s, each with its own seeded path (numpy rng, seed 7); both stack in landing order, 3 per layer.
- Result: Bolt drops at 2.0 s; Mochi leads until row 8 (321 vs 256); LEAD CHANGE row 9 at 7.40 (512 vs 340); first landing 8.32; centre bins FULL 8.98 → SPLIT WINS; Mochi then 392 on the board, 173 landed, centre bin 32 = 25 % of FULL; her gold dashed bell appears.
- Sound: galton_split2's (Campanella bells per row, firehose patter, landing ripple, G#-minor cadence on FULL).
- Checks (encoded Full HD, label b71): 743 f = 12.38 s; −14.00 LUFS, peak −5.7; flash PASS; seam 0.45. Frames read 0.3, 3, 6, 7.42, 8.4, 8.75, 9.0, 10.5.
- Doubts: 12.4 s (under the 15-17 s band); the first 5 s are quieter (−20.9 dB RMS) — only the patter + bed before the rows.
- Delivered review/batch71/galton_split3.mp4. Owner review: pending.

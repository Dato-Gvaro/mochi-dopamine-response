# ol_flag_colours3: a visible FEED (owner review docs/REVIEW_1114b.md: "flags appear too quickly and become balls")

- New file from ol_flag_colours2.py (v2 untouched). Patch: `output/tmp/builderF2/patch_flag3.py`.
- Feed = overhead conveyor line: rail at y 352, chain links (pitch 56), sprockets at x 34 / 1046
  (decoration zone), each flag hangs on 2 clips (top at y 376), rides in from the left edge, clips
  open above its landing x, it drops (5200 px/s²) to the plate and melts as v2. Empty clips ride on.
- Line speed V0 750 px/s x [1, 2, 4, 5] per rung (eased 0.22 s at each SPEED x2 pop), back to 1x
  over 1.2 s after the finale so the dissolve matches frame 0. 8x was feasible but flags crossed in
  ~0.09 s; 5x keeps a dense queue in the finale rung.
- Landing x: seeded greedy (`solve_feed`, restarts from seed 900): no two flags overlap on the line
  (gap 10 px) or on the plate (within 0.20 s rungs 0-1, 0.10 s rungs 2-3); bursts sweep right->left.
  Constraint: one serial line needs ~ (w + gap) / note gap px/s, so rung 0-1 flags shrank
  (RUNG_H 170/104/68/50 -> 110/84/58/46, WMAX 390/188/98/82 -> 230/150/88/76).
- On screen before release (median): rung 0 0.89 s, rung 1 0.38 s, rung 2 0.21 s, rung 3 0.13 s
  (v2: fall 0.26-0.32 s). Names ride above the line (rungs 0-1), sized never wider than their flag.
- SPEED x2 pop moved y 288 -> 266 (names above the line).
- Tally, 190 flags (no Russia/Belarus/Iran), USA first, music, drop times, finale: v2.
- Outcome: (fill after review)

## 4K ship (2026-11-14, shipper)
- 4K stills vs FHD 0.32-0.80 (edge AA only; no scale bug). Staged `DopamineExe\schedule\2026-11-22\1_ol_flag_colours3.mp4` (04:00 local Nov 23): 998 fr, -14.01 LUFS, TP -6.5, flash 0, seam 0.274, frames vs FHD 1.35-2.01.

# tug_war3 — 1,000 × 2ⁿ vs n!, the formulas big at the top (batch71)

- Brief: docs/BRIEF_batch71.md §3. New file `scenes/tug_war3.py` (from tug_war2; untouched).
- Changes: Bolt starts with 1,000 (B0 1000), N_DBL 11 steps (1.1 … 11.1 s, every downbeat); the factorial passes at step 10 (3,628,800 vs 1,024,000); LINES at the flag's position at T_LINE = T_LAST + 0.5 = 11.6 s (L_sim 7,428); L_PX 110 (was 80); the integrator uses 400 substeps/frame (10 blew up at these forces; same ODE x'' = K(right − left) − G v − BQ v|v|).
- Top: BOLT "1,000 × 2ⁿ" (superscript drawn) and MOCHI "n!", live values under (gold = the bigger), "n = k". tug_war2's caption + giant counts removed; the bottom counts removed (names, flag meter and ×2/×n badges stay).
- Result: flag −0.79 (79 % of the way to Bolt's LINE) at 10.10 s; FACTORIAL PASSES 10.1; LEAD CHANGE (centre) 11.18; over Mochi's LINE 11.60 → MOCHI WINS; pile lands 12.1 (cadence).
- Music: Danse napolitaine from score beat 80 (was 82) so it starts at frame 0.
- Checks (encoded Full HD, label b71): 870 f = 14.50 s; −14.01 LUFS, peak −5.6; flash PASS; seam 0.54. Frames read 0.3, 5, 9, 10.15, 10.6, 11.0, 11.25, 11.5, 11.65, 12.2, 13.5. (v1 render had LEAD CHANGE over the fading FACTORIAL PASSES; fixed: that pop ends before the lead change.)
- Delivered review/batch71/tug_war3.mp4. Owner review: pending.

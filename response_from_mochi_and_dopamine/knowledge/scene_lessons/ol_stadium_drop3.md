# ol_stadium_drop3 (DopamineEXE, owner review docs/REVIEW_1114.md)
- v3 of `ol_stadium_drop2` (v2 untouched). Owner 2026-11-14: at the end, clearly show how many doublings it took to overflow.
- ONE change: the small two-line recap (y 452) is replaced by a big STAMP on a dark plate with a gold rim, centred at y 640 over the flooded dome:
  - "OVERFLOWS AFTER" (50 px) / "46 DOUBLINGS" (gold, 132 px, fitted to 740 px) / "41 DOUBLINGS: ONLY 3.7% FULL" (36 px).
  - Lands 0.6 s after FULL (`--stamp-t`, after the geyser peak) with a 1.35x slam and a low "stamp" bloop (midi 31); held 2.1 s to the dissolve.
- FHD verified 2026-11-14: 11.57 s, -14.0 LUFS, peak -5.4 dBFS, flash PASS (2, as v2), seam 2.92 (as v2). Review: `<VIDEOS_DIR>\DopamineExeeviewol_stadium_drop3.mp4`.
- The numbers are computed, not typed: `N_DOUBLINGS = ceil(log2(D_FULL)) = ceil(45.743) = 46` (asserted 2^45 < D_FULL <= 2^46). After 45 doublings it is 59.7% full; the 46th takes it to 119%. `N_EARLY = N - 5 = 41`, 2^41 / D_FULL = 3.73%.
- Everything else is v2: facts (0.05 mL drop, 104,000,000 ft^3, D_FULL 58,899,040,911,360), camera, music, 11.57 s.

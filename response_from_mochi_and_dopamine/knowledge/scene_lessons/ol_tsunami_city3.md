# ol_tsunami_city3 (DopamineEXE, 2026-11-12, brief docs/BRIEF_1112b.md §2; v2 + owner notes)
- v2 city + HILL (345..483 x 909..1000, r22): a wall for the water, the buses' safe car park (spots x 382/410/438/466). T_FULL 12.0, clip 14.1 s.
- Buses: centre-line routes (Route = rounded polyline at 1 px). Cruise 50 → flee speed from t_e+0.12+0.07k. `solve_bus` grid-searches the start offset s0 (and, for "catch" targets, speed 54..v) against TR at back/centre/front. Outcome = first frame TR<=t, else the back on the hill.
- Seed 2 result: E 3.60 escape, B (hero 2) 9.38 escape with min margin 0.41 s at the breach, A (hero 1) 11.37 escape with 0.30 s. C1-4 caught 1.45, 4.18, 6.60, 8.70 (speeds 62-86).
- Cars: random walks on the street graph, right-hand lane (offset w/2-5.2). Rejected if one ever comes within CAR_LEN+1 of another car or (Lbus+Lcar)/2+3 of a bus while driving: 46 kept. 7 beach-road cars at y -575 for frame 0.
- Floats: drift along the TR gradient (34 → 7 px/s), spin, never enter a wall cell. Cars fade out 1.2-3.8 s after; buses stay. Keep the tint low (≤0.25) and add a white foam rim, or they vanish in the blue.
- People: r 4 white dots with a dark rim. n = min(roof cap 3/4/5, 2 + round(3u)), u = flood progress. Stagger 0.18 + (0.09+0.05u)k. One pitched pop per person (28 ms dedupe) makes the event rate climb (buildings reached per second is flat).
- Music: Strauss Thunder and Lightning (Mutopia 610), bars 1-4 + 5-20 + 57-58, FULL = bar 60. Tempo ramp x1.30 (~190 → 245 bpm). SFX pitched to the per-quarter harmony.
- Checks (FHD): −14.0 LUFS, TP −5.3, flash PASS (worst 2/s, the dissolve), seam 0.80.

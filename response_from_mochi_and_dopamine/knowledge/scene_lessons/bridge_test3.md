# bridge_test3: the MEDIEVAL canyon, stone ARCH vs steel TRUSS (batch27)

- **Why:** owner review of bridge_test2 (2026-10-11): "it's lava and it looks like a MEDIEVAL atmosphere, and those cars don't fit. Also let's have a DRAGON or dragon silhouette flying in the sky background."
- **Build:** `scenes/bridge_test3.py` imports `scenes/bridge_test2.py` (importlib) and swaps in, at run time:
  - `draw_obj`, `incoming`, `make_bg`, `near_layer`, `build_banners`, `draw_frame`;
  - the SIZE/LABEL/OFFS tables;
  - the pop and banner drawing.

  Everything else is bridge_test2's, unchanged: v1's physics (sim cached as `output/bridge_test3_sim_<key>.npz`), the time warp, the hook/rewind/loop, the camera, the characters and the orchestral bed with load-on-hit sync.
- **Gotcha:** when overriding a function that also calls the original, keep a reference to it BEFORE the swap (`_DRAW_OBJ2`, `_NEAR_LAYER2`); otherwise it recurses.
- **Loads (same tonnage, beats and slots):** hay cart 1 t; barrels 2 t; stone blocks 5 t; iron chests 10 t; bronze bells 15 t; catapults 20 t; war elephant (armour-plated, coral caparison, howdah) 25 t; CASTLE TOWER 75 t. The incoming target is a dashed tower silhouette.
- **Set:**
  - a stone keep with lit windows and a mint flag on the far mesa, right of the sun;
  - ruined crenellated walls on the far-left mesa and the far-right cliff;
  - 4 torches (two on the near cliff faces, two on the far cliffs), flickering with whole cycles over the clip;
  - waving mint pennants on the far cliffs (Bolt's side);
  - hanging coral banners on the near cliff faces (Mochi's side).
- **Dragon:** our own generic silhouette (bat wings, horned head, spade tail), dark plum with a faint sunset rim, wings flapping.
  - 3.6-11.2 s: left to right at y ≈ 338, span 140.
  - 17.6-24.0 s: right to left at y ≈ 396, span 112, with a soft, small fire-breath glow (0.4 s ramps, no flash).
  - The climax: a swoop at y ≈ 300-340, span 220, from T_FINAL + 0.55 on the loop-continuous clock. It is still in the sky at frame 0 and exits by T_END + 0.72 (before the rewind ends at T_END + 0.86).
  - It stays above the horizon and behind the bridges.
- **Pop banners:** they read from their first frame: alpha 1 on the first frame, scale 1.15 -> 1.0.
  - Sizes: pops 70; SNAP / HOLDS 76; INCOMING 72; COLLAPSE 86; TRUSS HOLDS 66.
- **Music:** as bridge_test2: Tchaikovsky, Piano Concerto No. 1, Op. 23, bars 1-16 (1875, PD), v1's score (midiworld tchai1-1.mid checked against IMSLP #916318), arranged with lib/orchestra.
- **Checks (Full HD, encoded):**
  - h264 yuv420p 1080x1920, 60 fps, 1657 frames = 27.62 s.
  - -14.01 LUFS; peak -5.43 dBFS; last 0.5 s -76 dBFS.
  - flash_check: 0 flashes = PASS (mean lum 0.074).
  - Seam step 5.3 sits inside its neighbours (3.3-5.4; the camera rumbles), so the turnaround is continuous.
  - Frames read at 0, 0.25, 0.5, 1, 2, 3, 7, 13.8, 16.3, 19.5, 24.82 and 26.3 s.
- **Delivered:** <VIDEOS_DIR>\batch27\bridge_test3.mp4 (Full HD). **Owner review:** pending.
- Owner review (2026-10-11): good -> APPROVED, 4K.

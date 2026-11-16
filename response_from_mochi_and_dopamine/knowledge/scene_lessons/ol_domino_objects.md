# ol_domino_objects (DopamineEXE, BRIEF_dopa_1113 clip 1)
- Sequel to ol_domino_giant (21K). One nameable change: every domino is a REAL thing. The chain runs from a dice to the Moon: 39 things, 38 hits, true sizes, ratios 1.2-2.5x (mean 1.7).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_domino_objects\` (FHD, 13.45 s, label fhd2). README there holds the rung table and sources.
- Reuse (read-only):
  - The R3 art comes from ol_domino3_objects, painted by an Aurora subclass on black.
  - From ol_domino_giant: text helpers, size units, clack, writer, and the Valkyries bed, sliced from bar 63 (`G.tb(9)`).

## How it works
- **Orientation per thing:** T (as drawn, topples), R (a long thing stood on its tail, nose up), B (rolls; collision shape = a circle of diameter = size).
- **Geometry:**
  - Convex hull of the drawing's flattened paths (FX parts excluded), oriented, normalised to back x 0 / bottom y 0.
  - Pivot = the front-most hull point within 3% of the bottom.
  - Gap after a thing: 0.45 x height (T/R) or 0.30 x diameter (B).
- **Lean:** largest angle with no overlap against the next thing's current pose (SAT polygon/polygon, polygon/circle). Scan 0.4° steps from the previous frame's angle, then bisect. Topples lift so no hull point goes below the ground.
- **Roll:** a ball rolls to its contact distance (scan + bisect; plain bisection fails because a far ball has passed THROUGH the next thing), then stops.
- **Simulation:** poses are simulated once for all frames; angles are warm-started, so they only grow.
- **Camera:**
  - log zoom follows the struck size (σ 0.22 s), anchor = the struck thing's back at x 300.
  - The zoom-out stops once the Moon is 560 px (`max(lz_chain, lz_moon)`). A zoom-IN to frame the finale is impossible under the monotone rule; clamp instead.
  - Then a sideways glide centres the Moon.

## Gotchas
- `S.dev_path` calls `identity_matrix()`, so the canvas scale must be multiplied into the object matrix (`.multiply(ctx.get_matrix())`). Without it, objects land off-screen at -Fast.
- Importing ol_domino_giant parses its flags (`--hold --hpx --bar --fin --sfx --cap`). This scene uses `--px --ax` to avoid the clash.
- The Golden Gate Bridge stood on end reads as a line, and the Asteroid trail / Halley coma FX don't suit a domino (dropped / stripped).

## Checks (fhd2)
- -14.0 LUFS, TP -6.2 dBTP; flash PASS (0).
- Seam 3.69 vs steps ~3.1-3.7.
- FHD render 53 s.

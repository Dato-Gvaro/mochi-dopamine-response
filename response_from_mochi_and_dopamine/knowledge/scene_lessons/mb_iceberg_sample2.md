# mb_iceberg_sample2: "Mochi & Bolt vs The Iceberg" v2 (16:9 SHORT test, 43.8 s)

- Brief: docs/BRIEF_1113b.md task A. Owner review: docs/REVIEW_1113.md. Concept: docs/BRIEF_iceberg_sample.md.
- v1 (`scenes/mb_iceberg_sample.py`) is untouched. v2 copies v1's object, tool, sky, label and berg-outline code read-only, so it stays reproducible on its own.
- Review: `<VIDEOS_DIR>\MochiAndBolt\review\iceberg_sample2\`, with the README (owner-facing), PROGRESS.md, the contact sheet and the 1:1 crops.

## Build
- **Fracture.**
  - Voronoi by half-plane clipping; every edge is tagged with its neighbour id. No new deps.
  - Cubes have 8-10 cells; core = the cells holding the object's centre/sides.
  - The berg has 54 cells: 40 small underside "band" seeds (dmin 46), 14 medium, 8 large.
- **Bolt.** Damage per cell. Cracks are drawn along that cell's real edges (double stroke). The cell detaches at hp as a rigid body: ballistic motion, spin, gravity 2200.
- **Mochi.**
  - Melt per cell, spread to exposed cells within `spread` (65/35).
  - A melting cell shrinks toward its longest still-frozen edge, rounded with Chaikin smoothing (1-2 passes).
  - At 85% melted it slumps off as slush: a splash, then a puddle.
- **Supports and finishes.**
  - Cube: anything not connected to a core cell falls.
  - Berg: anything cut off from its largest connected part falls. v1-style "anchor = all non-band cells" left a top piece floating; caught in a still.
  - The core is locked until ≤ 2 non-core cells remain (the reveal is a finish); then the remaining shell crumbles.
- **Drawing.** Intact cells are ONE fill path (no seams), with ink only on edges facing the outside, a gone cell, or a melting cell.
- **Targets.**
  - A target is the lowest exposed edge facing down or sideways.
  - The tool rest height is `contact - tip + gap`, clamped to between TOOL_Y and TOOL_Y - RISE (400).
  - A hit lands only when the tool is within 42 px and has arrived vertically.
- **Spacing rules** (all learned from stills):
  - shared blocks: Mochi keeps to the left half and Bolt to the right; contacts stay ≥ SHARE_GAP 80 apart;
  - MIN_SEP 270 between the characters;
  - an idle character stands ≥ IDLE_SEP 340 off;
  - wide tools float further out (`TOOL_DXK`: sun 128, drill 130; others 98);
  - stall breaker: a target with no hit for 1.6 s is banned for 1 s.
  - SHARE_GAP and MIN_SEP together change the sim a lot. 300/110 stalled L2/L3 (a cube took 12 s); 270/80 gave the same timeline as 250/46.
- **Chunk throws** are re-aimed (±v, 1.5v, 0.3v) so no path crosses a character. Slush with no clear path lands on the hot tool and turns to steam (17 of them).
- **Audio.**
  - Bach prelude_c; glassharp doubles the arpeggio notes.
  - Chunk off = a glass layer on its hit note. Landings are SFX-only (`note_gain` 0) and kept ≥ 12 ms from every other onset (PROTECT_NOTES); the minimum gap is 12.2 ms.

## Numbers (FHD, encoded)
- 43.77 s, 2626 frames, h264 yuv420p 1920x1080 60 fps.
- -14.0 LUFS, TP -3.2 dBTP, tail -90 dBFS.
- flash_check PASS: worst 1 flash per 1 s (12.8 s).
- Sim:
  - hits per 5 s: 16, 29, 21, 51, 43, 41, 50, 16 (TBC);
  - chunks off per 5 s: 4, 6, 6, 11, 8, 8, 7;
  - lowest ice L1/L2/L3: 563 / 706 / 751 (heads 890);
  - final 7,213 / 6,755 pts; berg HP 43%.
- Renders: FHD took about 3.5 min; the FAST clip about 1 min; `--plan` takes 1.7 s.

## Timeline
See the review README (the per-second log is the output of `python scenes/mb_iceberg_sample2.py --plan`).

## Commands
```powershell
$env:TEMP='<REPO>\output\tmp'; $env:TMP=$env:TEMP
python scenes/mb_iceberg_sample2.py --plan
$env:NF_FAST='1'; python scenes/mb_iceberg_sample2.py --still --frame 0s,4.3s,13.2s,21s,33s,36.8s; Remove-Item Env:NF_FAST
# full renders: take output/render.lock first
$env:NF_SCALE='1.0'; python scenes/mb_iceberg_sample2.py --label fhd1 --review
```

## Lessons
- Read stills for **tool spacing on shared blocks**. Two tools between two characters is the crowding failure. It is never a limb, but it reads as clutter.
- A tool wider than ~80 px needs a bigger side offset, or it touches the body at rest (pocket sun, drill).
- Crate objects must sit ~20 px above the crate front, or flat objects (the fish) vanish.
- The heat glow follows Mochi's target only while her tool is under it (otherwise it lights the wrong block).

## Open
- Owner questions: L1 length (reveal at 4.2 s), tools floating up to 400 px, rack capacity for 8-10 min, boss end HP.

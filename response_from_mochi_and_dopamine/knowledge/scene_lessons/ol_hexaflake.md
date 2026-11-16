# ol_hexaflake (DopamineEXE) — franchise episode of ol_sierpinski
- Batch 65. ONE nameable change vs the 18.6K triangle: **HEXAGONS** (the hexaflake, a snowflake). Same look, HUD, gloss, crack-and-drop, dust rain, glitter + shimmer, pour-down finale, dissolve loop.
- Engine: `lib/splitdust.py` + `lib/flake2d.py` (see docs/scenes/ol_pentaflake.md); scene file = geometry + score + arrangement.
- Caption (baked, `--cap`): `Every hexagon ^SPLITS^ into 7|until it turns to ^DUST^`.
- Delivered for review: `<VIDEOS_DIR>\DopamineExe\review\batch65\ol_hexaflake.mp4` (Full HD, seed 3, label fhd, 15.55 s). No 4K yet.

## Maths (honest)
- A flat-top regular hexagon splits into 7 hexagons a third its size: one at each corner + one in the middle (they touch only at tips). What is left = 12 equilateral triangles (2 per edge: one on the edge's middle third, one against the centre hexagon) = 2/9 of the area, which drop out. Verified numerically (0 mismatches).
- Count = 1 + 6 per split = 7^n; 7 gens -> **823,543**. AREA LEFT (live) = (7/9)^n -> **17.2%** at DUST, then the share of the dust still on screen -> 0% during the pour.

## World
- Circumradius 385, centre (508, 760): x 123-893 (inside 0.10-0.84 w), y 427-1093. Outline 2.5 px white 85%.
- Tile height per gen: 237, 79, 26, 8.8, 2.9, 0.98, 0.33 px: gens 6-7 = DUST (glitter boost from gen 6).
- Fallers: gens 1-3 textured triangles (gens 1-2 grow toward the viewer), gen 4 solid (4,116 small triangles), gens 5-7 dust dots. Cracks gens 1-4.

## Clock = the score
- `Clock` tau 20: 2.02 -> 3.67 beats/s; DUST beat 33 at 12.00 s. GEN_BEATS 0, 1, 2, 5, 13, 21, 27; DUST 33.

| Gen | Splits | Window (s) | Splits/s |
|---|---|---|---|
| 1 | 1 | 0.05 | |
| 2 | 7 | 0.54-0.90 | 15 |
| 3 | 49 | 1.02-2.28 | 36 |
| 4 | 343 | 2.39-5.54 | 106 |
| 5 | 2,401 | 5.63-8.35 | 859 |
| 6 | 16,807 | 8.43-10.22 | 9,008 |
| 7 | 117,649 | 10.29-11.93 | 68,943 |

## Timeline
- 0.00 whole glossy rainbow hexagon, 1 HEXAGONS, GEN 0/7, AREA LEFT 100%, DUST mark (a 49-dot hexaflake). 0.05 crack + the G-sharp octave; 0.12 the 12 triangles drop.
- 0.6 s: 13 hexagons, gen 2 cracking; 1.2 s: 91, a rain of triangles; 3 s gen 4 (~769), the snowflake shape readable; 7 s gen 5 (~10K).
- 12.00 DUST: 823,543, AREA LEFT 17.2% (gold), glitter + shimmer. 12.70 the dust pours down. 14.95 dissolve into frame 0. 15.55 s, 933 frames.

## Sound
- **Melody:** Chopin, Fantaisie-Impromptu in C-sharp minor Op. 66 (1834, pub. 1855; PD). The opening G-sharp octave (sf) on the first crack, then bars 5-12 (score beats 16-48: right-hand semiquaver cascades over left-hand triplets) from clip beat 1; bars 11-12 sit on the dominant G-sharp and DUST is the C-sharp-minor tonic they lead to. Source: Mutopia-2009/09/05-1693 (Scholtz edition, Public Domain), `<SOUNDFONTS_DIR>\scores\chopin_fantaisie_impromptu\`. Not used on DopamineEXE before (Mochi: galton_split, sort_wheel …). Not kid-coded.
- Arrangement: piano plays every note (RH brighter, LH softer, + a low bass octave each half bar), strings + cello + contrabass sustain the half-bar bass, celesta on the RH beat heads from clip beat 9, tubular bells on the G-sharp and phrase heads, timpani on gen starts, soft boom on the first crack; DUST = rolled C-sharp-minor tutti + timpani roll; the fall = harp + celesta cascade.
- 193 note slots, every one on a split (max offset 0.049 ms). Notes/s **7, 13, 14, 15, 15, 15, 18, 17, 19, 19, 20, 21** (climbs the whole clip). 766 SFX events.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 933 frames, 15.55 s. **flash_check PASS** (0 flashes, mean lum 0.028).
- **-14.01 LUFS**, peak -4.8 dBFS, last 0.5 s digital silence. RMS/s -17.7 -18.1 -21.0 -19.0 -20.8 -21.3 -18.4 -18.8 -18.0 -15.3 -17.1 -15.7, DUST -14.2, fall -15.5.
- Seam (check_clip): mean |Δ| **0.200**.
- Frames read from the mp4 at 0, 0.6, 1.2, 3, 7, 12, 13.2, 15.53 s; 1:1 crops at 0.6 s (cracks + textured triangles) and 3 s (gen-4 tiles + triangle rain).

## Doubts
- The C-sharp-minor DUST chord is the same chord as the triangle's (Rachmaninoff was also C-sharp minor).
- 4-6 s is the quietest stretch (RMS -21 dB) while gen 4 runs 3.2 s.
- Gen 6-7 are sub-pixel: glitter, as in the triangle.

## Flags
`--seed (3) --label --cap --still --frame --dry --sound 0 --sfx (0.30) --fin (3.2) --tdust (12) --tau (20) --rad (385)`.

## v2 --zoom (2026-11-01, owner: "after half it's hard to tell the difference, maybe we zoom in to show more details and at the end zoom out")
- Engine (`lib/flake2d.py`, opt-in; v1 bit-reproducible without `--zoom`): `Zoom` = camera zoom z(t) about a fixed screen point P chosen so a level-2 tile (`--ztile` corner digit, middle child) lands exactly on the flake at full zoom Z = (1/r)^2; log z eases in over `--zin a,b`, holds, eases out over `--zout c,d` (default 11.35,12.2: whole flake back for DUST, before the pour at T_D+0.7). Crispness: K+1 `Fractal` levels (window P + (E-P)/Z_j, sampled at sc·Z_j, Z_j = Z^(j/K), K = ceil(ln Z / ln 1.45) = 6), each ~12.5 s to build at Full HD (~75 s total, ~0.5 GB); a frame upsamples its level <= 1.45x, the hold is 1:1. Window E = flake bbox + 60/30 px; the flake image, outline, zoom pieces and dust stay inside E, the big (gen <= 4) fallers keep falling below it. Gap pieces of the gens between solid_max and the last (`Zoom.pieces`, own RNG 1000+seed: sim timing and notes untouched) are drawn as solid triangles while zoomed; the last gen stays dust dots (size up to 2 px). Live gold "ZOOM ×n" tag at E's top-left.
- Profile (2026-11-01, Full HD): base Fractal 27 s (12 s alone), world draw ~0.37 s/frame; zoomed frames similar (one level's state() per frame). Full render ~9 min.
- (depth-2 first pass, superseded) Hexagon: Z 9 about (796.8, 760.0) (corner 0's middle child), in 6.0 -> 10.3 s, out 11.35 -> 12.2 s; zoom pieces gen 5: 18,384, gen 6: 8,760. At the hold gen 7 tiles are 26 px (crisp at 1:1).
- (superseded, archived) depth-2 render (label zoomv2): 933 frames, -14.01 LUFS, peak -4.78, last 0.5 s silent, flash 0, seam 0.20, events json identical to fhd. Weak: the zoomed region is mostly blue-violet (rainbow by position).
- First render had the level image spilling below E over the meter (clip bug, fixed before delivery; the bad file is output/ol_hexaflake_zoomv2_rejected_9x16.mp4).
- **Shipped depth 3** (`--zdepth 3`, default): Z 27 about (774.5, 760.0), 9 levels; zoom pieces gen 5: 16,200, gen 6: 1,416, gen 7: 5,568. At the hold gen-6 tiles are 26 px, splitting into 8.8 px. Gloss fix: `Fractal(zk=Z_j)` scales the rim widths to the on-screen size (without it, zoomed tiles washed out silver). The depth-2 (×9) render above was superseded before review (newest splits only 2.9-8.8 px; archived `ol_hexaflake_v2_zoom-x2gen_unreviewed.mp4`). Final `review\batch65\ol_hexaflake_v2.mp4` (label zoom3): 933 frames, -14.01 LUFS, peak -4.78, flash 0, seam 0.20, events identical.
- **STAGED 4K v1, no zoom** (2026-11-02, owner preferred v1 over the zoom): `--label h4k` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-15\2_ol_hexaflake.mp4` (events json byte-identical to fhd). 2160x3840 h264 yuv420p 60 fps, 933 frames, -14.01 LUFS, peak -4.78, flash PASS (2 in the pour at 13.4 s; Full HD had 0), seam 0.12.

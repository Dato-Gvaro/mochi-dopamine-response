# ol_pentaflake (DopamineEXE) — franchise episode of ol_sierpinski
- Batch 65. ol_sierpinski = the channel's only hit (18.6K), carpet 4.2K; owner approved franchising. ONE nameable change: **PENTAGONS** (Dürer's pentaflake). Same look, HUD, gloss, crack-and-drop, dust rain, glitter + shimmer, pour-down finale, dissolve loop.
- Engine: `lib/splitdust.py` (HUD, clock, score snap, SFX, mix, render loop: extracted from the triangle/carpet, which stay untouched) + `lib/flake2d.py` (generic polygon n-flake: exact per-pixel raster, 3x3 supersampled, gap-piece fallers). Scene file = geometry + score + arrangement.
- Caption (baked, `--cap`): `Every pentagon ^SPLITS^ into 6|until it turns to ^DUST^`.
- Delivered for review: `<VIDEOS_DIR>\DopamineExe\review\batch65\ol_pentaflake.mp4` (Full HD, seed 3, label fhd, 15.55 s). No 4K yet.

## Maths (honest)
- A regular pentagon splits into 6 pentagons scaled r = 1/(1+φ) = 0.382: one at each corner (homothety at the vertex) + one upside down in the middle; they touch along edges. What is left = 5 **golden triangles** (36-72-72), 12.46% of the area, which drop out. Verified numerically (Monte-Carlo, 0 mismatches between "not in a child" and "in a gap triangle").
- Count = 1 + 5 per split = 6^n; 8 gens -> **1,679,616**. AREA LEFT (live) = 0.8754^n -> **34.5%** at DUST, then the share of the dust still on screen runs to 0% during the pour (carpet rule).

## World (logical 1080x1920)
- Pentagon circumradius 400, centre (508, 800): x 128-888 (inside 0.10-0.84 w), y 400-1124. Outline 2.5 px white 85%.
- Tile height per gen: 283, 108, 41, 15.8, 6.0, 2.3, 0.88, 0.34 px: gens 7-8 are sub-pixel = DUST (glitter; coverage shown ^(1-0.5·ramp) from gen 7 as in the triangle).
- Fallers: gens 1-3 the golden triangles textured from the parent's shading (gens 1-2 grow x1.1/s toward the viewer), gen 4 solid, gens 5-8 dust dots (one per split, ~4,000 sampled per gen). Cracks (gap edges drawn in) gens 1-4.

## Clock = the score
- One smooth accelerating tempo (`Clock`, tau 20): 1.96 -> 3.56 beats/s, DUST beat 32 at 12.00 s.
- GEN_BEATS 0, 0.75, 2, 4, 12, 20, 24, 28; DUST 32.

| Gen | Splits | Window (s) | Splits/s |
|---|---|---|---|
| 1 | 1 | 0.05 | |
| 2 | 6 | 0.43-1.00 | 10 |
| 3 | 36 | 1.05-1.92 | 38 |
| 4 | 216 | 2.00-5.30 | 63 |
| 5 | 1,296 | 5.40-8.22 | 446 |
| 6 | 7,776 | 8.31-9.54 | 5,941 |
| 7 | 46,656 | 9.61-10.77 | 37,978 |
| 8 | 279,936 | 10.84-11.91 | 241,869 |

## Timeline
- 0.00 whole glossy rainbow pentagon, 1 PENTAGONS, GEN 0/8, AREA LEFT 100%, DUST goal mark (a 36-dot pentaflake). 0.05 first crack; 0.12 the 5 golden triangles drop.
- 0.5 s: 11 pentagons, the big triangles tumbling out; 1.0 s 36; 2.0 s gen 4 (~221); 7 s gen 5, the snowflake fully readable.
- 12.00 DUST: 1,679,616, AREA LEFT 34.5% (gold), glitter + shimmer, mark pops. 12.70 the dust pours down (bottom first). 14.95 -> 0.6 s dissolve into frame 0. 15.55 s, 933 frames.

## Sound
- **Melody:** Paganini, Caprice No. 24 in A minor, Op. 1 (c.1817, pub. 1820; d. 1840, PD): the Tema as the Mutopia MIDI unfolds it (bars 1-4, 1-4, 5-12 = score beats 0-32), DUST on beat 32 (the A that opens Var. I). Source: Mutopia-2015/03/25-2000 (Ricordi; engraving CC BY-SA 4.0, notes PD), `<SOUNDFONTS_DIR>\scores\paganini_caprice24\`. Not used on DopamineEXE before (Mochi: mousetrap_chain). Not kid-coded.
- Harmony added (the theme is unaccompanied): Am E Am E (x2), A7 Dm G7 C Dm6 Am E7 Am, one chord per 2-beat bar.
- Arrangement: piano melody + pizzicato doubling, celesta / harp on the long notes from bar 5, strings chord pad, cello + contrabass + piano bass on the bar, tubular bells, timpani on each gen start, soft boom on the first crack, timpani roll into DUST; DUST = rolled A-minor tutti; the fall = harp + celesta A-minor cascade.
- 84 note slots, every one on a split (max offset 0.050 ms). Notes/s 6, 7, 6, 2, 7, 9, 4, 8, 10, 8, 10, 7.
- SFX: the triangle's glassy tinks (pitch range mapped over 8 gens), 813 events.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 933 frames, 15.55 s. **flash_check PASS** (0 flashes, mean lum 0.043).
- **-14.01 LUFS**, peak -5.1 dBFS, last 0.5 s digital silence. RMS/s -17.7 -17.9 -19.0 -21.3 -18.7 -19.2 -19.4 -19.0 -16.6 -15.9 -15.8 -16.7, DUST -14.4, fall -15.7.
- Seam (check_clip): mean |Δ| **0.205** (the dissolve ends on frame 0).
- Frames read from the mp4 at 0, 0.5, 1, 2.5, 7, 12, 13.2, 15.53 s; 1:1 crops at 1.0 s (golden triangles, gloss) and 7 s (gen-5 tiles crisp).

## Doubts
- Paganini's long notes leave thin seconds (3 s: 2 notes; RMS -21.3 dB). The tinks keep the split rate climbing.
- Gen 4 holds 3.3 s (216 splits): the slowest stretch after the 2 s burst.
- The pentagon shrinks faster per gen (x0.38) than the triangle (x0.5): only 6 visible gens, gens 7-8 are glitter.

## Flags
`--seed (3) --label --cap --still --frame a,b --dry --sound 0 --sfx (0.30) --fin (3.2) --tdust (12) --tau (20) --rad (400)`.

## v2 --zoom (2026-11-01, owner: "after half it's hard to tell the difference, maybe we zoom in to show more details and at the end zoom out")
- Engine (`lib/flake2d.py`, opt-in; v1 bit-reproducible without `--zoom`): `Zoom` = camera zoom z(t) about a fixed screen point P chosen so a level-2 tile (`--ztile` corner digit, middle child) lands exactly on the flake at full zoom Z = (1/r)^2; log z eases in over `--zin a,b`, holds, eases out over `--zout c,d` (default 11.35,12.2: whole flake back for DUST, before the pour at T_D+0.7). Crispness: K+1 `Fractal` levels (window P + (E-P)/Z_j, sampled at sc·Z_j, Z_j = Z^(j/K), K = ceil(ln Z / ln 1.45) = 6), each ~12.5 s to build at Full HD (~75 s total, ~0.5 GB); a frame upsamples its level <= 1.45x, the hold is 1:1. Window E = flake bbox + 60/30 px; the flake image, outline, zoom pieces and dust stay inside E, the big (gen <= 4) fallers keep falling below it. Gap pieces of the gens between solid_max and the last (`Zoom.pieces`, own RNG 1000+seed: sim timing and notes untouched) are drawn as solid triangles while zoomed; the last gen stays dust dots (size up to 2 px). Live gold "ZOOM ×n" tag at E's top-left.
- Profile (2026-11-01, Full HD): base Fractal 27 s (12 s alone), world draw ~0.37 s/frame; zoomed frames similar (one level's state() per frame). Full render ~9 min.
- (depth-2 first pass, superseded) Pentagon: Z 6.85 about (508.0, 510.6) (top corner's upside-down middle child), in 6.0 -> 9.6 s (`--zin 6.0,9.6`), out 11.35 -> 12.2 s; zoom pieces gen 5: 2,855, gen 6: 4,745, gen 7: 13,480. At the hold gen 7 tiles are 41 px and gen 8 tiles 15.8 px.
- (superseded, archived) depth-2 render (label zoomv2): 933 frames, -14.01 LUFS, peak -5.10, last 0.5 s silent, flash PASS (2 general flashes, worst 1/s at 8.38 s), seam 0.21, events json identical to fhd. Weak: zoomed region mostly green.
- **Shipped depth 3** (`--zdepth 3`, default): Z 17.94 about (508.0, 538.2), 8 levels; zoom pieces gen 5: 2,505, gen 6: 1,210, gen 7: 2,380, gen 8: 14,120. At the hold gen 7 splits 41 -> 15.7 px, gen 8 15.7 -> 6.0 px. Depth-2 render superseded before review (archived `ol_pentaflake_v2_zoom-x2gen_unreviewed.mp4`). Final `review\batch65\ol_pentaflake_v2.mp4` (label zoom3): 933 frames, -14.01 LUFS, peak -5.10, flash PASS (2 general flashes, worst 2/s at 7.73 s), seam 0.21, events identical.
- **STAGED 4K v1, no zoom** (2026-11-02, owner preferred v1 over the zoom): `--label pe4k` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-16\1_ol_pentaflake.mp4` (events json byte-identical to fhd). 2160x3840 h264 yuv420p 60 fps, 933 frames, -14.01 LUFS, peak -5.10, flash PASS (2 in the pour at 13.4 s), seam 0.13.

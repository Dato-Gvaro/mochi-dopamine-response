# ol_sierpinski_pyramid (DopamineEXE) — franchise episode of ol_sierpinski
- Batch 65. ONE nameable change vs the 18.6K triangle: **a 3D PYRAMID** (regular tetrahedron = the Sierpinski tetrahedron), slowly turning. Same HUD, colours, crack-and-drop, dust rain, glitter + shimmer, pour-down finale, loop.
- Caption (baked, `--cap`): `Every pyramid ^SPLITS^ into 4|until it turns to ^DUST^`.
- Delivered for review: `<VIDEOS_DIR>\DopamineExe\review\batch65\ol_sierpinski_pyramid.mp4` (Full HD, seed 3, label fhd, 15.55 s). No 4K yet.
- Why the pyramid and not the Menger cube (both were offered): "Every cube SPLITS into 27" would be dishonest in the series' own convention (the count is the survivors: 7 of 27 fall out, the counter would run x20). The tetrahedron keeps exactly the hit's structure (split into 4 corners + the middle falls out, x4) in 3D. The cube stays a possible later episode titled "into 20" (or "into 27… 7 fall OUT").

## Maths (honest)
- Each tetrahedron: cracks along the lines joining its edge midpoints; the middle **octahedron** (half the volume) drops out; 4 half-size tetrahedra stay at the corners. Count 4^n; 9 gens -> **262,144**. VOLUME LEFT (live) = 0.5^n -> **0.20%** at DUST; during the pour it is the share of the dust still on screen -> 0%.

## Renderer
- Orthographic; the object turns about its vertical axis at 0.42 rad/s under a fixed 22° tilt (camera slightly above). Edge 720 logical px, centroid (508, 820): turning, it spans x <= 148-868 (inside 0.10-0.84 w), y ~410-1112.
- All pyramids are translates of one shape: per frame each level's sprite (visible faces, Lambert from the upper left + an edge rim highlight) is rasterised once and stamped back-to-front (painter's order: depth of the cell at level g-1, then own depth), 2x2 supersampled (1x at 4K). Levels with <= 64 elements are rasterised per element with sub-pixel position and a per-pixel rainbow (object-space hue, so frame 0 is a full rainbow); deeper levels use one colour per element.
- Edge per gen: 360, 180, 90, 45, 22.5, 11.2, 5.6, 2.8, 1.4 px: gen 9 = DUST.
- Fallers: gens 1-5 the octahedra themselves (shaded faces, hairline white edges, spin about a random axis, gravity, drift toward the viewer: drawn in front); gens 6-9 dust dots (one per split, sampled ~4,000/gen). Cracks (the midpoint triangle on each visible face) gens 1-5. White container wireframe (visible edges) all clip, fades during the pour.
- Loop: the dissolve brings in the clip's own t<0 (the whole pyramid, still turning), so the last frame flows into frame 0 (`render(..., preroll=True)`).

## Clock = the score
- `Clock` tau 20: 1.96 -> 3.56 beats/s; DUST beat 32 at 12.00 s. GEN_BEATS 0, 0.5, 2, 4, 8, 12, 16, 20, 24; DUST 32.

| Gen | Splits | Window (s) | Splits/s |
|---|---|---|---|
| 1 | 1 | 0.05 | |
| 2 | 4 | 0.30-0.99 | 5 |
| 3 | 16 | 1.05-1.92 | 17 |
| 4 | 64 | 2.00-3.63 | 36 |
| 5 | 256 | 3.77-5.30 | 157 |
| 6 | 1,024 | 5.40-6.78 | 680 |
| 7 | 4,096 | 6.91-8.22 | 2,924 |
| 8 | 16,384 | 8.31-9.51 | 12,517 |
| 9 | 65,536 | 9.61-11.86 | 27,468 |

## Timeline
- 0.00 whole rainbow pyramid turning, 1 PYRAMIDS, GEN 0/9, VOLUME LEFT 100%. 0.05 crack, 0.12 the big octahedron drops out toward the viewer.
- 0.4 s: 7 pyramids, the octahedron in front; 1.0 s: 16, four octahedra tumbling; 2.5 s gen 4 (124); 5 s gen 5/6, the tetrix clearly 3D with pits and tunnels, small octahedra raining.
- 12.00 DUST: 262,144, VOLUME LEFT 0.2% (gold), glitter + shimmer, mark pops. 12.70 the dust lets go, bottom first, while it turns. 14.95 dissolve into the turning whole pyramid. 15.55 s, 933 frames.

## Sound
- **Melody:** Mozart, *Die Zauberflöte* K.620 No. 14 "Der Hölle Rache" (1791; PD): the coloratura, score beats 92-124 (held A, the run to eight staccato C's, eight A's, the D run, the F-major arpeggios to high F twice), DUST on beat 124 = the F-major chord the run lands on. Full score, every part read. Source: Mutopia-2013/03/24-266 (Peters 1875 etc.; Public Domain), `<SOUNDFONTS_DIR>\scores\mozart_queen_night\MF14-ArieScore.mid`. Not used on DopamineEXE before (Mochi: press_drill). Not kid-coded. (The Magic Flute's Egyptian temple setting suits a pyramid.)
- Arrangement: the Queen's line on flute + piano (+ celesta an octave up on the staccatos from beat 4), the orchestra parts on strings / cello / contrabass / oboe / bassoon / horns / trumpet / timpani as written, tubular bells on phrase heads, timpani on gen starts, soft boom on the first crack; DUST = rolled F-major tutti + timpani roll; the fall = harp + celesta F-major cascade.
- 73 note slots, every one on a split (max offset 0.049 ms). Notes/s 4, 8, 4, 5, 5, 8, 5, 7, 8, 6, 7, 6. 612 SFX events (glassy tinks, landing ticks, glitter).

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 933 frames, 15.55 s. **flash_check PASS** (0 flashes, mean lum 0.024).
- **-14.00 LUFS**, peak -5.1 dBFS, last 0.5 s digital silence. RMS/s -17.3 -18.4 -18.1 -17.9 -20.4 -18.6 -19.2 -19.9 -19.0 -18.3 -18.4 -17.3, DUST -14.3, fall -14.9.
- Seam (check_clip): mean |Δ| **0.430** (good band; the object is turning, the step is one frame of rotation).
- Frames read from the mp4 at 0, 0.4, 1, 2.5, 5, 8, 12, 13.2 s; 1:1 crops at 0.4 s (octahedron + faces) and 5 s (gen-5/6 pits crisp).
- Render: ~1.1 s/frame at Full HD (~17 min); 4K uses ss 1 (similar pixel work).

## Doubts
- Every ~5 s (the 3-fold symmetry: 2π/3 at 0.42 rad/s) a face turns to the camera and the pyramid reads as a flat Sierpinski TRIANGLE (~2.5, ~7.5, ~12 s = DUST): the "3D" is clearest in between. More tilt (`TILT`) or a slower turn would keep it 3D longer.
- Note density is the lowest of the three (4-8/s); the tinks carry the climb.
- The octahedra are one flat hue each (not textured like the 2D fallers).
- The pour (12.7-14 s) is a dense grain cloud, less shapely than the 2D pours.

## Flags
`--seed (3) --label --cap --still --frame --dry --sound 0 --sfx (0.30) --fin (3.2) --tdust (12) --tau (20) --edge (720) --omega (0.42)`.

- **STAGED 4K** (2026-11-01): `--seed 3 --label k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-12\2_ol_sierpinski_pyramid.mp4` (events json byte-identical to the reviewed Full HD). 2160x3840 h264 yuv420p 60 fps, 933 frames, -14.00 LUFS, peak -5.06, flash 0, seam 0.38. Full HD -> archive/ol_sierpinski_pyramid_fhd.mp4.

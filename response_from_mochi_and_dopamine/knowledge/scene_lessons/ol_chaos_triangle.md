# ol_chaos_triangle (DopamineEXE, batch62 #5)

## v1 (2026-10-31)
The chaos game, exact. Three corner pegs (red bottom-left, green apex, blue bottom-right) on ol_sierpinski's triangle (side 780, apex (508, 420)). A die picks a corner (1-2 red, 3-4 green, 5-6 blue; the faces are drawn next to each peg) and the next dot lands exactly halfway between the last dot and that corner. The first 6 jumps are drawn slowly (rolling die → dashed line to the corner → arc → "½" tick); then the total doubles every 2 triplet notes up to 100,000 dots, and the Sierpinski triangle appears. Finale: a shimmer sweep, the empty middles (levels 1-3) tinted and outlined, "dots in the holes: 0".

- Caption (baked; `--cap ''` = base): `Every dot jumps ^HALFWAY^ to a random corner…|until a ~PATTERN~ appears`. True: every dot is the exact midpoint; the pattern appears.
- "dots in the holes: 0" is COUNTED (barycentric test against every removed triangle down to level 12, open holes, tolerance 1e-9), not asserted. It is exactly 0 because the walk starts ON the red peg (a vertex), so there is no transient: every dot lies on the fractal. (Starting from a random interior point would leave ~8 transient dots in holes.)

## Model
- `pts[i+1] = (pts[i] + corner[roll[i]]) / 2`, rolls from `np.random.default_rng(24)` (seed 24: the first rolls 3, 2, 5, 3, 5, 4 visit all three corners and never the same corner twice in a row in the opening). Corner shares at 100k: 33,067 / 33,407 / 33,526.
- Counts N_k = round(100,000 / 2^(14−k)): 6, 12, 24, 49, 98, 195, 391, 781, 1,562, 3,125, 6,250, 12,500, 25,000, 50,000, 100,000 (×2 per step). Dots of a step land uniformly inside its 2-triplet window.
- Dot colour = 0.62 × the corner jumped to + 0.28 × the previous + 0.10 × the one before (HSV S 0.75): the three big sub-triangles come out red / green / blue with nested mixes, an ordered gradient.
- Dot radius 9 → 1 px (9·(6/N)^0.33); cairo discs up to 1,500 dots, then a bilinear splat + Gaussian (σ 0.55 r) per frame.

## Timeline (Consolation No. 3 triplets at 74 bpm, T3 = 0.2697 s)
- Jumps 1-6 land at 0.10, 0.37, 0.64, 0.91, 1.18, 1.45 s (frame 0: dot 1 mid-arc toward green, die settling on 3).
- Doublings every 0.539 s from 1.99 s; 1 s ≈ 4 dots, 2.5 s 23, 4 s 171, 5.5 s 1,192, 7 s 8,120, 8.5 s 53,699; **100,000 at 9.00 s**.
- 9.0 shimmer sweep apex → base (0.6 s); 9.4 holes tinted + "dots in the holes: 0"; dissolve 10.4-11.0 into frame 0. **11.0 s, 660 frames.**

## Screen
- Die (92 px) top-left of the triangle with ROLL / ROLLING (+ "n rolls/s", true rate) / DONE; peg labels (die face + "1-2" / "3-4" / "5-6") inside x 0.10-0.84w.
- Meter y 1300: JUMPS on a log scale (×10 per mark: 1 · 10 · 100 · 1K · 10K · 100K, gold goal at 100K from frame 0). Counter y 1500: DOTS (gold at 100,000, auto-shrinks to fit), ×2 pill above-right on each doubling. Watermark 35%.

## Sound
- F. Liszt, Consolation No. 3 in D-flat, S. 172 (1850, PD), Mutopia (engraving CC BY 3.0, PD notes only), `<SOUNDFONTS_DIR>\scores\liszt_consolation3\SOURCE.txt`, read at runtime. Score beats 10-21 at 74 bpm: the LH triplet arpeggio carries the jumps (jumps 1-6 = its six triplet notes, a warm pluck doubles each), the theme enters on jump 4; piano + cello an octave down + soft strings, D-flat pedal (contrabass + strings). The reveal (beat 21) = a rich D-flat chord (strings, piano, harp roll, celesta, soft timpani). Replaces the brief's Borodin "Gliding Dance" (no PD score data on Mutopia; IMSLP has no MIDI/MusicXML).
- SFX: soft glassy ticks per landing (D-flat pentatonic, MIDI 70-87, ≥16 ms apart, gain ∝ 1/√density).

## Checks (encoded mp4, output/ol_chaos_triangle_fhd_9x16.mp4)
- h264 yuv420p 1080x1920 60 fps, 660 frames, 11.00 s; **-14.00 LUFS**, peak -6.92 dBFS, last 0.5 s digital silence; flash_check PASS (0); seam mean |Δ| 0.157.
- Stills read at 0, 0.2, 0.75, 1.6, 2.5, 4, 5.5, 7, 8.5, 9.1, 9.8, 10.7 s; 1:1 at 9.13 s, 10.0 s and the counter at 8.5 s.

## Flags
`--seed` (24), `--label`, `--cap`, `--still --frame`, `--dry`, `--audio`, `--sfx`, `--sound 0`.

## Upload draft
- `Jump halfway to a random corner… until a pattern appears 🔺 #satisfying #physics #shorts`
- `Random dice rolls, 100,000 times: this is what appears 🔺 #satisfying #physics #shorts`
- `Roll a die, jump halfway, repeat. Wait for it 🔺 #satisfying #physics #shorts`
- Pinned: `it's all random dice rolls and not one dot lands in a hole. how?`

## v2 (2026-11-01, owner review: "text does not show why it appeared")
- `--v2`: a persistent WHY under the triangle from 1.7 s (after the 6 slow jumps): "each dot jumps ^HALFWAY^ to a corner," / "so it can ^NEVER^ land in a hole" (y 1186/1228, 32 px). The first two jumps' ½ ticks also say "HALFWAY" in gold. Fades with the dissolve (frame 0 has no WHY: clean loop).
- Deliverable `<VIDEOS_DIR>\DopamineExe\review\fixes_1101\ol_chaos_triangle_v2.mp4`. 11.00 s, -14.00 LUFS, peak -6.92, silent tail, flash 0, seam 0.16. v1 -> archive/ol_chaos_triangle_v1.mp4.

- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-15\1_ol_chaos_triangle.mp4` (events json byte-identical to the reviewed Full HD). 2160x3840 h264 yuv420p 60 fps, 660 frames, -14.00 LUFS, peak -6.92, flash 0, seam 0.09. Full HD -> archive/ol_chaos_triangle_v2.mp4.

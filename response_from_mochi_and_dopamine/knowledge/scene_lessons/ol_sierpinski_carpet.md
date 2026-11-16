# ol_sierpinski_carpet (DopamineEXE, channel 2) — franchise sequel of ol_sierpinski
- Batch 52 (docs/BRIEF_batch52.md). ol_sierpinski = the channel's breakout (17.3K, 10× the rest). ONE nameable change: **SQUARES** (the Sierpinski carpet). Built as a copy of `scenes/ol_sierpinski.py` (that file is untouched and stays bit-reproducible); same look, HUD, colours, gloss, crack-and-drop, dust rain, glitter + shimmer, pour-down finale, dissolve loop.
- Caption (baked, `--cap`; `--cap ''` = base): `Every square ^SPLITS^ into 9… the middle falls ^OUT^|until it turns to ^DUST^` (the coordinator's wording). Line 1 is long, so it auto-fits at ~34 px vs line 2's 54 px. A balanced alternative: `--cap "Every square ^SPLITS^ into 9…|the middle falls ^OUT^ until ^DUST^"`.
- Delivered (v1, review): Full HD, seed 3, label fhd, 15.65 s; that file is archived as `DopamineExe\archive\ol_sierpinski_carpet_fhd.mp4`.
- **Shipped (2026-10-28, batch 53): with the BROOM ending, 4K** → `<VIDEOS_DIR>\DopamineExe\schedule\2026-10-29\1_ol_sierpinski_carpet.mp4` (label ship). Everything up to the dust's fall is unchanged.

## Broom ending (owner, 2026-10-27: "after it becomes dust, it piles on the floor and a broom swipes 2-3 times and clears it")
- `--broom 1` (default); `--broom 0` = the v1 ending (grains fade below the square, 15.65 s).
- **Floor**: a white line at y 1186 (x 40-1040, 55%), between the square (bottom 1113) and the HUD (GEN / AREA LEFT labels at ~1230); it fades in as the dust lets go (12.5-13.0 s).
- **The dust lands**: every falling grain keeps its fall (same physics) until it reaches the floor (its exact landing time/x solved per grain), then joins the **pile**: a 1-D granular height field (2 px bins, mean layer 13 px) that relaxes to an angle of repose (0.42), with a colour per bin (mass-weighted). The last grain lands at 14.65 s.
- **The broom** (drawn: wooden handle with a highlight, a red binding band, a fan of 26 straw bristles that trail the stroke): enters in the air from the left at 14.40 s, then 3 strokes along the floor (head front, ease slow-fast-slow): 14.78-15.22 s x 90→520, 15.46-15.90 s x 380→790, 16.14-16.62 s x 660→1210 (off the right edge); lifts (≤ 62 px) and swings back between strokes; exits right by 16.92 s.
  - Each stroke pushes everything under the 96 px head to its front as a wedge at the repose slope (so the layer gathers into a growing heap ahead of it); mixed dust shows as a speckled rainbow (grains of every colour); 3.5%/frame of the pushed dust puffs up as soft pastel clouds (55 puffs).
  - Dust pushed past x 1080 is gone. **AREA LEFT** keeps counting the dust on screen (falling + piled): 39.0% while it lies on the floor, → 37.5% (puffs) → 18.8% mid stroke 3 → **0% when the floor is clean (16.45 s)**.
- Clean floor held to 17.04 s, then the 0.6 s dissolve into frame 0. **17.63 s, 1,058 frames** (v1 15.65 s: +2.0 s).
- Sound: the music is untouched (its DUST chord + harp/celesta cascade end by ~15 s, i.e. it lets the broom play in near silence); each stroke = a soft swish (band noise 500-3,200 Hz following the stroke's slow-fast-slow speed, a 38-48 Hz bristle flutter); the clean floor = 2 soft glass glints (A6, E6) at 16.64 s.
- 4K encoder now uses `rc-lookahead=12` (shared laptop).

### Checks (encoded 4K ship, broom ending)
- h264 High yuv420p **2160x3840**, 60 fps, 1,058 frames, 17.63 s. **flash_check PASS**.
- **-14.01 LUFS**, peak -3.85 dBFS, last 0.5 s digital silence. RMS per 0.25 s over the broom (14.0-17.0 s): -12.4, -13.5, -19.7, -21.9, -22.9, -33.7, -21.7, -30.9, -40.5, -22.0, -25.0, -28.2 (the swishes sit ~-22 dB, soft).
- Seam: mean |Δ| 0.139 (check_clip); luma last→0 0.089.
- Frames read from the mp4 at 0, 5, 12.0 (DUST), 13.2, 14.3, 14.9, 15.15, 15.6, 15.95, 16.4, 16.8 and 17.6 s; a 1:1 crop at 15.15 s (broom bristles, the wedge of dust ahead of it, puffs, AREA LEFT 38.3%). The 4K render took ~20 min.
- Staged: `DopamineExe\schedule\2026-10-29\1_ol_sierpinski_carpet.mp4` + slot 1 of that folder's UPLOAD.md (pinned comment now mentions the sweep).

### Doubts (broom)
- The pushed dust's back face stands vertical against the bristles (nothing flows under the head) and the puffs trail behind the broom rather than ahead of it.
- The music has ended by the time the broom sweeps (swishes in near silence): the owner allowed "keep the music or let it end".
- Not owner-reviewed as a clip: the brief approved shipping it straight to 4K.

## World (logical 1080x1920)
- One square, side **729 = 3^6**, x 144-873 (inside 0.10-0.84 w), y 384-1113. Thin white outline 2.5 px, 85%, kept for the whole clip.
- Fill: the triangle's glossy rainbow by position (hue across x, a little by height, red bottom-left → violet right, same perceptual warp; HSV S .75 V 1). Every square has its own gloss in its own coordinates: lighter toward the top, bright left and top rims, a sheen streak near the left edge, darker bottom and right rims. Gloss fades out below ~3 px.
- Exact geometry: the side is pixel-aligned, so at Full HD a gen-6 square is exactly 1 px. Per pixel (lattice coordinates): the generation where it falls into a middle and that middle's drop time, down to level 6; generations 7-8 (1/3 px and 1/9 px) are added as exact area fractions (1/9 at gen 7, 8 × 1/81 at gen 8, each at its own drop time). No supersampling, no moiré. Fast (0.5) uses 2×2 samples at the logical pixel centres (also exact); 4K would use 3×3 and level 7.
- The split: hairline white cracks open the 3×3 grid (the middle's outline first, then out to the edges; gens 1-4), then the middle drops out. Fallers:
  - gens 1-3: the dropped middle itself, textured from the parent's shading, white hairline edge, spin + gravity 2,200 px/s² + a small outward/up kick, growing ×1.1/s (falling toward the viewer);
  - gens 4-5: solid squares in their colour;
  - gens 6-8: dust (1 px dots; air drag, terminal 420-760 px/s, wobble, twinkle; a random 1 in 8 / 64 / 512 drawn, ~4,100 per generation; life 1.6 s).
  - Pieces dim to 35% as they fall past the HUD band.
- HUD (the triangle's, unchanged in style): meter y 1252 (rainbow fill, white marker, **8 rungs**, "GEN n / 8", pale-gold DUST mark = a tiny 2-level carpet + label). Counter y 1478: true count (1 + 7 per split = 8^n after gen n), "SQUARES", "×8" pill in the generation hue that pops on each generation start and on DUST; the number auto-shrinks from ~1.5M up so it stays inside the side band. **AREA LEFT** (new, live from frame 0, right above the meter): the true area, 100% → 88.9 → 79.0 → … → **39.0%** at DUST (turns pale gold); then, as the dust pours away, it is the share of the dust still on screen and runs down to **0%** (the nod to the triangle comment "Area left = 0%. You just stopped early."). Watermark "DOPAMINE.EXE" (900 right, 1338), 35%.

## Clock = the score
- Generation k starts on clip beat `GEN_BEATS[k-1]` = 0, 0.5, 1, 2, 3, 6, 12, 15; DUST on beat 24 (the A-minor tonic).
- Beat → time: one smooth accelerating tempo, b(t) = R0·τ·(e^((t−0.05)/τ) − 1), τ 16 s, R0 1.35 beats/s → 2.85 at DUST (12.00 s). Smooth on purpose: the tremolo stays even.
- Splits inside a generation run as a diagonal wave (top-left → bottom-right), spread over 92% of its window. Every score slot is snapped onto a split (monotone). Gen 1's middle drops on the first tremolo note (beat 1/8, 0.142 s). Max note → split offset 0.049 ms.

| Gen | Splits | Window (s) | Splits/s | Squares after | Area left |
|---|---|---|---|---|---|
| 1 | 1 | 0.05 | | 8 | 88.9% |
| 2 | 8 | 0.42-0.75 | 22 | 64 | 79.0% |
| 3 | 64 | 0.77-1.41 | 92 | 512 | 70.2% |
| 4 | 512 | 1.47-2.08 | 772 | 4,096 | 62.4% |
| 5 | 4,096 | 2.13-3.90 | 2,226 | 32,768 | 55.5% |
| 6 | 32,768 | 3.97-7.06 | 10,416 | 262,144 | 49.3% |
| 7 | 262,144 | 7.12-8.43 | 191,652 | 2,097,152 | 43.8% |
| 8 | 2,097,152 | 8.48-11.96 | 596,366 | **16,777,216** | **39.0%** |

## Timeline (clip s)
- 0.00 the whole glossy square, 1 SQUARES, GEN 0/8, AREA LEFT 100%. **0.05** the first crack (the 3×3 grid opens), **0.14** the big middle drops and tumbles out.
- **0.5 s**: 22 squares, gen 2: the big middle falling and spinning; the top row of the 8 has cracked, their middles dropping.
- **1.0 s**: 225 squares, gen 3: 8 middles falling; 9-tile blocks forming.
- **2.0 s**: 3,641 squares, gen 4: the 2-level carpet, gen 3-4 squares rain to the sides and down.
- ×8 pops at 0.05, 0.42, 0.77, 1.47, 2.13, 3.97, 7.12, 8.48 s.
- 5 s: ~114K squares, gen 6, the full carpet readable (1 px holes forming), dust rain.
- 7-12 s: gens 7-8 are sub-pixel: the carpet dims slightly (shown at coverage^0.55 so it reads as glitter) while the counter runs into the millions.
- **DUST 12.00 s**: 16,777,216 squares, AREA LEFT 39.0% (gold). Glitter + shimmer sweep top → bottom (0.55 s), DUST mark pops.
- **12.70 s: the dust falls.** Every pixel of the DUST carpet becomes a 2 px grain and lets go, bottom rows first, the top last (0.65 s × height + 0.1 s jitter); gravity 1,050-1,500, drift σ 22 px/s, flutter; grains fade between y 1173 and 1593. AREA LEFT runs 39.0% → 0%. Empty outline by ~15.0 s.
- 15.05 → 0.6 s dissolve into frame 0. **15.65 s, 939 frames.**

## Sound
- **Melody:** Francisco Tárrega, *Recuerdos de la Alhambra* (1896; Tárrega d. 1909, PD), the opening tremolo theme: bars 1-5 and 9-11 (bars 6-8 restate 4-5 and are cut), then the A-minor tonic on DUST (bar 11's E major → A minor, where the piece itself returns home). Bar 1's 2nd/3rd tremolo notes are omitted (the first middle is falling). 191 note onsets, each on a split. Source: Mutopia "Mutopia-2009/05/09-810" (Orfeo Tracio edition; engraving CC BY-SA 3.0, notes PD), `<SOUNDFONTS_DIR>\scores\tarrega_recuerdos\recuerdos.mid` + `info.html`. Not on any used list (BRIEF_batch50/51/52, docs/scenes/*.md), not kid-coded, not banned. Mood match: like the triangle's Rachmaninoff, a minor-key late-Romantic piece; its shimmering tremolo IS the glitter of the dust.
- Notes per second: 9, 12, 13, 13, 14, 15, 17, 17, 18, 20, 20, 23 (rising with the tempo).
- Arrangement: harp plays the tremolo an octave up (the shimmer), piano the bass + arpeggio + the first note of each tremolo group, strings sustain the melody line (+ oohs from bar 5), cello + contrabass on the bass, celesta on the tremolo heads from beat 6, tubular bells on every bar's downbeat (bar 1 loud), timpani on gens 1-3 (bar 1) and every later generation start, a soft boom on the first crack, a timpani roll into DUST.
- DUST: rolled A-minor tonic (A1-E5) + strings, oohs, contrabass, tubular bells A4/A3, timpani A2, a soft boom; glass glitter tinks on A-minor tones; the fall = a falling harp + celesta A-minor cascade from 12.7 s.
- SFX (the triangle's): a glassy tink per split (bell partials, all < 5.5 kHz), pitch rising and decay shortening with the generation (640 Hz/45 ms → ~1.8 kHz/16 ms at gen 8), every split ticked while sparse, then sampled ≥ 12 ms apart (+0-16 ms random when dense), gain ÷ √(rate/10). Tinks per second 22, 44, 49, 45, 49, 51, 47, 43, 45, 49, 52, 44. A 4-tick crunch on the first crack; soft landing ticks as gen 1-5 pieces leave the frame.
- `audio.master(peak_db=None, reverb=0.5)`, sfx ×0.30, `--fin` 3.2. Last 0.6 s digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 939 frames, 15.65 s. **flash_check PASS** (0 flashes, mean lum 0.046).
- Audio (muxed mp4): **-14.01 LUFS**, peak -4.1 dBFS, last 0.5 s digital silence; energy > 6 kHz 0.03%. RMS per second -15.7 (opening), -21.3, -21.1, -20.1, -20.3, -20.2, -18.3, -18.2, -16.6, -17.7, -16.7, -15.2, DUST -11.8, the fall -12.5, -16.6. No second below -24 dB.
- 191 note onsets, each on a split (max offset 0.049 ms; beat 1/8 = the first drop). 730 SFX events.
- Seam (encoded, check_clip): mean |Δ| **0.204** (the dissolve ends on frame 0).
- Frames read from the mp4 at 0, 0.5, 1, 2, 5, 8, 12 (DUST), 13.17, 13.83 s and the last frame; 1:1 crops at 5 s (the 1 px gen-6 holes stay crisp after encoding) and 13.17 s (the bottom crumbling into grains while the top carpet still stands).

## Doubts
- Caption line 1 is long (the brief's wording) and renders at ~34 px; the balanced alternative is above.
- Gens 7-8 are finer than a pixel: they read as the carpet dimming into glitter, not as separate splits (as gens 8-10 did in the triangle). The carpet loses area slowly (×8/9 per generation), so at DUST 39% is left vs the triangle's 5.6%: the "dust" is the sub-pixel size of the squares and the pour-down, not an empty-looking frame. AREA LEFT reaching 0% during the pour is the share of the dust still on screen (honest: the frame is empty), not the math limit.
- Recuerdos is a guitar piece; here it is harp + piano + strings. Gentler and less "grand" than the triangle's Rachmaninoff.

## Flags
`--seed (3) --label --cap --capw (790) --still --frame a,b,c --dry [--audio] --sound 0 --sfx (0.30) --fin (3.2) --broom (1; 0 = the v1 fade-out ending)`. Clock: `--tdust (12.0) --tau (16.0)`. Geometry: `--side (729) --top (384)` (exactness needs side 729 at Full HD). The seed only moves the wave jitter, the fallers' kicks/spins and the dust samples.

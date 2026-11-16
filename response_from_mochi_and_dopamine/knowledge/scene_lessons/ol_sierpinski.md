# ol_sierpinski (Overflow Lab, channel 2)
- New scene, character-free (docs/BRIEF_channel2.md). Owner direction 2026-10-21: "use more math, splits, exponents, triangles". Skeleton: ×3 growth toward a named end state (research/early_breakouts.md; the parent's 1.85M "Every ball crushed splits into 3"). The Sierpinski triangle as a physical shattering: every triangle cracks, its middle quarter drops out and falls, leaving 3 corners, until the pieces are DUST.
- Opening follows the owner's ol_crack_ice note: a clean, readable frame 0, a strong effect inside 2 s (generations 1-4), then the steady build, accelerating into the finale.
- Caption (baked, `--cap`; `--cap ''` = base): `Every triangle ^SPLITS^ into 3|until it turns to ^DUST^`. Highlights in the current generation hue. DUST was picked over "until 59,049 triangles": a stranger can picture dust muted in 2 s; the number reads on the counter.
- Delivered: `<VIDEOS_DIR>\channel2\ol_sierpinski.mp4` (**v2**, Full HD, seed 3, label fhd2, 15.55 s). No 4K yet.
- Owner review 2 (2026-10-22): "make the dust fall down at the end instead of swiping to the side" → v2: the DUST fractal pours DOWN under gravity (no wind). Also the channel Colour rule (docs/BRIEF_channel2.md): saturation 0.85 → **0.75** everywhere (tiles, fallers, meter, badge); every falling piece keeps its position hue, so the rain is the same ordered gradient (no random hues); the pale-gold DUST mark is the one warm accent.

## World (logical 1080x1920)
- One equilateral triangle, side 780, apex (508, 420), base y 1095 (x 118-898, inside 0.10-0.84 w). Thin white outline 2.5 px, 85%, kept for the whole clip (the container).
- Fill: glossy rainbow by position (hue across x, a little by height, red bottom-left → violet bottom-right, perceptually warped so green doesn't take half the frame; HSV S .75 V 1). Every tile has its own gloss in its own coordinates: lighter toward the apex, a bright left rim, a sheen streak, darker base and right rims. Gloss fades out once a tile is < ~3 px tall, so each new corner looks like a small copy of the big glossy triangle.
- Exact geometry: per pixel (3×3 supersampled, lattice coordinates), the generation where it falls into a middle quarter and the drop time of that quarter. A frame of the fractal is one threshold on those times, so every generation stays crisp, including the 0.76 px triangles of gen 10.
- The split: hairline white cracks run between the parent's 3 side midpoints (gen 1: 0.06 s, shorter later; none from gen 7), then the middle drops out. Fallers:
  - gens 1-5: the dropped quarter itself, textured from the parent's shading, white hairline edge, spin + gravity 2,200 px/s² + a small outward/up kick (gens 1-3 also grow ×1.1/s, falling toward the viewer);
  - gens 6-7: solid triangles in their colour;
  - gens 8-10: dust (1 px dots; air drag, terminal 420-760 px/s, wobble, twinkle; gen 9 drawn 1 in 2, gen 10 1 in 5, life 1.6 s).
  - Pieces dim to 35% as they fall past the HUD band so the counter stays the focus.
- HUD (same look as ol_spiral_center): meter y 1252 (x 170-846, rainbow fill, white marker, 10 rungs = the generation ladder, "GEN n / 10" above it, pale-gold DUST mark = a tiny dot Sierpinski + label from frame 0). Counter y 1478: true count (1 + 2 per split = 3^n at the end of gen n), "TRIANGLES", "×3" pill in the generation hue that pops (×1.3, τ 0.1 s) on each generation start and on DUST. Fact line "AREA LEFT 5.6%" (= 0.75^10) above the meter from DUST + 0.15 s. Watermark "OVERFLOW LAB" (900 right, 1338), 35%.

## Clock = the score
- Generation k starts on beat `GEN_BEATS[k-1]` of the score: 0, 1, 2 (bar 1's A, G#, C#), 8, 12, 18, 24, 32, 40, 46; DUST on beat 54 (bar 14's C#).
- Beat → time: anchors (0, 0.05 s), (1, 0.42), (2, 0.80), (8, 1.30), (12, 2.00), then an accelerating tempo 2.44 beats/s × e^((t−2)/10) to beat 54 at **12.00 s** (`--tdust`, `--tau`).
- Splits inside a generation run as a diagonal wave (apex first, top-left → bottom-right), spread over 92% of its window (gen 2: 45%). Every score slot is snapped onto a split (monotone), so every note lands on a split (max offset 0.05 ms).

| Gen | Splits | Window (s) | Splits/s | Triangles after |
|---|---|---|---|---|
| 1 | 1 | 0.05 | | 3 |
| 2 | 3 | 0.42-0.59 | | 9 |
| 3 | 9 | 0.80-1.26 | 18 | 27 |
| 4 | 27 | 1.30-1.94 | 39 | 81 |
| 5 | 81 | 2.00-4.03 | 37 | 243 |
| 6 | 243 | 4.20-5.86 | 135 | 729 |
| 7 | 729 | 5.99-7.87 | 367 | 2,187 |
| 8 | 2,187 | 7.98-9.54 | 1,321 | 6,561 |
| 9 | 6,561 | 9.63-10.63 | 6,057 | 19,683 |
| 10 | 19,683 | 10.72-11.92 | 15,342 | **59,049** |

## Timeline (clip s)
- 0.00 the whole glossy triangle, counter 1, GEN 0/10. **0.05** the first crack (white hairlines between the side midpoints), 0.11 the middle drops.
- **0.5 s**: 5 triangles, gen 2; the big middle quarter is falling and spinning out of the bottom; the top corner has just split.
- **1.0 s**: 17 triangles, gen 3; three falling quarters, a 9-tile triangle forming.
- **2.0 s**: 83 triangles, gen 5 starting; gen 4's 27 small quarters rain down the screen.
- ×3 pops at 0.05, 0.42, 0.80, 1.30, 2.00, 4.20, 5.99, 7.98, 9.63, 10.72 s.
- 6 s: 735 triangles, gen 7, the full Sierpinski readable, a rainbow rain of small triangles under it.
- 8-12 s: gens 8-10 turn to dust; coverage drops to 5.6%, shown slightly brighter (coverage^0.5) so it reads as glitter, not fading.
- **DUST 12.00 s**: 59,049 triangles. Glitter + a shimmer sweep apex → base (0.55 s), DUST mark pops, "AREA LEFT 5.6%".
- **12.70 s: the dust falls.** Every pixel of the DUST fractal becomes a 2 px grain in its own colour and lets go: the bottom rows first, the apex last (release 0.65 s × height + 0.1 s jitter). Gravity 1,050-1,500 px/s², a 0-70 px/s start, a slow sideways drift (σ 22 px/s) and a small flutter. The grains fade out between y 1155 and 1575 (below the triangle, before the counter). The fractal crumbles from the bottom up into a rainbow cascade; empty outline by ~14.6 s.
- 14.95 → 0.6 s dissolve into frame 0 (the whole triangle). **15.55 s, 933 frames.**
- v1 (superseded): a sideways wind from 12.8 s, dissolve 14.55, 15.15 s / 909 frames.

## Sound
- **Melody:** Rachmaninoff, Prelude in C-sharp minor Op. 3 No. 2 (1892; d. 1943, PD), bars 1-13 (beats 0-54), all onsets of both hands = 98 score slots, read from the MIDI. Bar 1's three "bells" A - G# - C# land on generations 1, 2, 3 (fff, with tubular bells and timpani); bars 3-13 (the Lento chords over the bass motif) walk one slot per sampled split. Bar 13 ends A - G#, and bar 14's C# is DUST. Source: Mutopia "Mutopia-2015/07/09-2033" (Bosworth 1896 / UE 1910; engraving CC BY-SA 4.0, notes PD); `<SOUNDFONTS_DIR>\scores\rachmaninoff_prelude_csharp_minor\` + `SOURCE_mutopia_2033.txt`. Not on the used list, not kid-coded, not banned.
- Notes per second: 3, 11, 6, 5, 7, 7, 7, 9, 9, 10, 12, 12 (the burst, then rising).
- Arrangement: piano (opening fff, rings ≥ 1.1 s; then the chords crescendo), tubular bells on every bass-motif note (bar 1 loud, then soft), strings on the bass octaves, contrabass, celesta on the chord tops from beat 18, oohs on the bass from beat 24, timpani on bar 1's three bells and on each generation start, a soft boom on the first crack, a timpani roll into DUST.
- DUST: rolled C#-minor tonic (C#1-G#4) + strings, oohs, contrabass, tubular bells C#3/C#4, timpani C#3, a soft boom; glass glitter tinks on C#-minor tones; the fall = a falling harp + celesta C#-minor cascade from 12.7 s (no whoosh).
- SFX: a glassy tink per split (bell partials 1 / 2.32 / 2.76, all < 5.5 kHz; 1.5 ms soft click; small body). Pitch rises and decay shortens with the generation (640 Hz/45 ms at gen 1 → ~1.8 kHz/16 ms at gen 10). Every split is ticked through gen 5, then sampled ≥ 12 ms apart with a random 0-16 ms extra gap when dense (no 83 Hz buzz), gain ÷ √(rate/10). A 4-tick crunch on the first crack. Landing ticks (low-passed, soft, ≥ 14 ms apart) when gen 1-6 pieces leave the bottom of the frame.
- `audio.master(peak_db=None, reverb=0.5)`, sfx ×0.30, `--fin` 3.2. Last 0.6 s digital silence.

## Checks (encoded Full HD, v2)
- h264 yuv420p 1080x1920, 60 fps, 933 frames, 15.55 s. **flash_check PASS** (0 flashes, mean lum 0.014; the triangle is only ~13% of the screen, so it can never make a large-area flash).
- Audio (muxed mp4): **-14.01 LUFS**, peak -5.6 dBFS, last 0.5 s digital silence; energy > 6 kHz 0.03%. Late body 9-11.9 s -18.1 dB RMS, DUST 12-13.5 s -15.7 (+2.4 dB), the fall 12.7-14.5 s -16.9.
- 98 notes, each on a split (max offset 0.05 ms). 647 SFX events.
- Seam (encoded, check_clip): mean |Δ| **0.157**: the dissolve ends on frame 0 itself.
- Frames read from the mp4 at 0, 1, 2, 7.5, 12.0 (DUST), 13.17 and 13.83 (the fall) s and the last frame; 1:1 crop of the fall at 13.17 s (the bottom tiers crumbling into grains while the apex fractal still stands).

## Doubts
- The Prelude is dark (C-sharp minor, bells). It is grand rather than creepy, but it is the least "sunny" piece on the channel so far.
- Gens 8-10 are finer than a pixel at Full HD: they read as the fractal dimming into glitter, not as separate splits. That is the DUST idea; the counter and tinks carry the ×3. In 4K gen 8 is still visible as triangles.
- 2-4 s (gen 5, the Lento chords at their quietest) is the calmest stretch after the burst (-20 dB RMS).

## Flags
`--seed (3) --label --cap --still --frame a,b,c --dry --sound 0 --sfx (0.30) --fin (3.2)`. Clock: `--tdust (12.0) --tau (10.0)`. Geometry: `--side (780)`. The seed only moves the wave jitter and the fallers' kicks/spins.

Owner review 2 (2026-10-22): "make the dust fall down at the end instead of blowing to the side" -> rework the finale.

Owner review 3 (2026-10-22): "ok".

Owner review 4 (2026-10-22): ok -> Dopamine.exe schedule.

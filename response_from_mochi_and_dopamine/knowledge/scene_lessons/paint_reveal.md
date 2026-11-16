# paint_reveal
- New scene (batch40). **PURE MECHANIC, no characters.** Research recipe: the progress meter IS the picture. Caption (baked, `--cap`; `--cap ''` = base): `Every bounce paints ^ONE^ pixel|~Until the masterpiece appears~`. The one readout above the frame: `PAINTED n%` -> `ONLY n LEFT` (gold, pulsing, from 9 left) -> `PAINTED 100%` (gold pop). The painting is never named on screen; the pinned comment names it.

## The image (rule 1 + 4: our rendering, PD target)
- Vincent van Gogh, *The Starry Night* (1889; van Gogh d. 1890) — public domain.
- Source: Wikimedia Commons `File:Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg` (Google Arts & Culture / MoMA scan, 44567x35291), licence tag **{{PD-Art|PD-old-100-expired}}** (API: LicenseShortName "Public domain", Copyrighted False). Downloaded the 1920 px thumbnail: `https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg/1920px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg`.
- Target = `assets/paint_reveal/starry_night_54x50.png`: crop x 290-1910, y 8-1508 of the 1920x1520 image (cypress, swirl, stars, MOON, village), LANCZOS-downscaled to 54x50. Rebuild: `python scenes/paint_reveal.py --build-grid <jpg>`. Graded at load: saturation x1.35, value contrast x1.25, floor 0.10 (the cypress stays above the dark tiles).
- **Deviation from the brief:** the crop is near-square (1.08 w/h), not a 4:5 portrait. The safe zone caps the frame at ~900-1000 px tall anyway, and a 4:5 crop would lose the moon (the most recognisable element). The cypress' left edge is trimmed instead.
- Every frame is code: rounded tiles (18 px) in the grid colours; the finale "smooth" image is the same 54x50 colours bicubic-upscaled. The photo never appears.

## World (logical px)
- Frame x 54-1026 (0.9 w), y 374-1274 (bottom 0.664 h), 54 x 50 = 2700 tiles of 18 px. Caption y 172/241, readout y 330.
- Unpainted tile: small dark rounded tile (0.055, 0.06, 0.08) + 0.30 x its target colour = a dim ghost; the end state reads at frame 0.
- Painted tile: full-size rounded tile in its colour + a faint top highlight. A paint = 0.15 s pop (1.38x -> 1x, whitened -> true colour) + 2 tiny paint droplets.
- Rendering: three pre-rendered layers (dark, painted, smooth) + a per-tile A8 mask (NEAREST) per frame; pops, hunt, balls are vector on top. Full HD render + sound ~3 min, one process.

## Physics (one model; px, s) — last_brick's engine, tiles instead of bricks
- Balls (R 7) at constant 1000 px/s; elastic reflection off the frame walls.
- An UNPAINTED tile is solid: a ball touching it reflects off it and paints it — **one tile per contact** (the deepest), so the caption is literal. Painted tiles are open space.
- **v2 (coordinator 2026-10-17: no slow start).** Start: 9 painted patches (moon, big star, swirl, hills, light band, 3 stars, village; radii 3.6-6.6 tiles, jagged by seed) = 734 tiles (27.2%). 16 balls, 2 per patch in the first 8 patches. Pre-roll 0.5 physics s: **30.1% painted at frame 0, 44% at 3 s**; the first paint is on frame 0.
- Escalation: at 550 / 1150 / 1650 painted, EVERY ball splits (+-0.5 rad): 16 -> 32 -> 64 -> 128.
- Substep 1/480 s, recorded 240/s. Mild 0.5x on the final tile (no slow-motion finish).
- Seed 4 (chosen from 4 for the hunt):

| Event | Clip s |
|---|---|
| splits ->32/64/128 | 3.89 / 8.09 / 12.48 |
| 50% / 90% painted | 4.32 / 12.98 |
| 10 left / 3 left / 1 left | 19.52 / 20.81 / 21.44 |
| last tile (0, 49) | 22.19 |
| clip end | 26.10 |

- Paints per 2 s: 272 211 328 247 282 197 173 91 51 28 | 6 1 (the hunt). With the dense start the paint rate peaks early and falls as the open picture leaves fewer unpainted boundaries. The escalation the eye sees is the ball count (16 -> 128) and the meter.
- (v1, seed 2: 12% at frame 0, 4 balls, 5 splits to 128, 30.47 s. Rejected for a slow start.)
- Hunt: the last 10 tiles pulse gold (ghost brightened, gold rim + glow); with <= 3 left, gold rings point at each.
- **Finale:** gold glow + 4 gold rings from the last tile; balls burst into sparks (wave from the last tile); tiles melt into the smooth bicubic image (1.1 s); zoom out 1.0 -> 0.94 over 2.4 s; a gold frame rim fades in; 12 star twinkles (4-point sparkles on the sky's brightest grid points), each twice. Final tile + 3.3 s -> 0.6 s dissolve into the pre-roll = loop.

## Sound
- **Melody:** Beethoven, Piano Sonata No. 14 "Moonlight", Op. 27 No. 2, 3rd mvt (Presto agitato; 1801, Beethoven d. 1827 -> PD). Notes read with `orc.read_midi` from the Mutopia Project MIDI (BeethovenLv/O27/moonlight, `moonlight3.mid`, cached `<SOUNDFONTS_DIR>\scores\beethoven_moonlight3\`; the sort_wheel source).
  - Bars 1-8, then bars 13-14 (a cut: bars 9-12 sit on the same G# pedal as bar 13), then the tonic downbeat of bar 15 as the cadence. That is 136 merged onsets from both hands.
  - Transposed down a whole tone (B minor): the highest note is B5 (83), nothing above C6. Soundfont piano (MuseScore_General, MIT).
- **Sync:** every note IS a painted tile (snapped to a real paint time, >= 55 ms apart).
  - Phrase starts at bars 3/5/7 land on the 3 splits. Bars 7-8 run 1.12x the bars 5-6 pace.
  - Bar 13 (the dominant alternation) is a ritardando through the hunt.
  - The bar-14 dominant chord lands on "3 LEFT" and its low octave on "1 LEFT". Both hold, with a soft strings_slow F#7 swell, until the final tile.
  - The final tile lands the B-minor cadence: a B1+B2 bass octave, a rolled B-minor chord up to D5, a strings + soft choir swell, and a soft timpani B.
- Notes per 2 s: 17 14 15 14 14 15 14 15 | 7 7 4 (steady ~7.5/s, then a ritardando over the hunt). Gaps: min 0.092 s, median 0.131 s.
- **SFX:** a soft paint "dab" per painted tile (3 modes at 640-1060 Hz by tile brightness with a 4 ms upward glide, a 2 ms 0.5-1.8 kHz click), merged within 12 ms into one fuller dab, density-aware level g = 0.55 (1 + rate/25)^-0.5; a bubble pop per split; a soft glass ping (B4/D5/F#5/B5) per twinkle. Every onset >= 12 ms apart and >= 12 ms off the piano notes. No hiss, whoosh or bed.
- Mix: bed (orc.render, -20 LUFS) + SFX x 0.22 -> `audio.master(reverb 0.4, peak_db -5)`, last 1.0 s digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx --peak`; physics `--v --splits`; `--build-grid <jpg>`.

## Checks (encoded Full HD, v2 seed 4)
- h264 yuv420p 1080x1920, 60 fps, 1566 frames = **26.10 s**.
- -13.99 LUFS, peak -7.60 dBFS (decoded mp4). The last 1.0 s is digital silence.
- flash_check PASS: 0 flashes (mean luminance 0.037).
- Seam: pre-encode last -> 0 has a mean delta of 0.564 vs a normal step of 0.593, so it is exact. Encoded: 1.66, from the I-frame on a busier frame 0.
- SFX events/5 s: 277 264 199 78 | 18. 818 dabs; every onset >= 12 ms apart.
- Encoded frames read at 0, 1, 2, 3, 15, 20.9, 22.3 and 24.5 s:
  - Frame 0: moon, swirl, stars and big star glowing on the ghost grid, 16 balls moving.
  - 15 s (95%): the painting is unmistakable.
  - "ONLY 2 LEFT" reads, with a gold ring on the last tile (bottom-left corner).
  - 24.5 s: the smooth image, gold rim and twinkles.
- Safe zone: caption y 172-245, readout 330, frame y 374-1274 (0.664 h). The moon is in the right strip but at ~0.2 h, above the Shorts buttons.
- Delivered Full HD as `<VIDEOS_DIR>\batch40\paint_reveal.mp4` (v2 replaced v1). Owner review: pending.

## Doubts
- **Falling paint rate:** with 30% pre-painted, the paint rate peaks in 0-10 s and falls after it (rule: the rate should still climb). The ball count and the meter carry the escalation. The hunt from 10 left lasts 2.7 s.
- **Hunt:** 3 LEFT lasts ~0.6 s and 1 LEFT ~0.75 s (+ the 0.5x).
- The last tile is the bottom-left corner (dark cypress), so its pop is less bright than a sky tile's would be.
- 128 balls at the end (the brief said ~64); fewer drags out the last 10%.
- The finale's smooth image is a bicubic upscale of the 54x50 grid colours: soft and painterly, not photo-sharp (by design: still our rendering).
- Moonlight 3rd mvt is also sort_wheel's music. Clair de Lune (cached) was rejected as too calm for an accelerating note stream; its tied, rubato melody doesn't survive an even accelerando.
- I have not listened to the audio; I checked it by numbers only (LUFS, HF share, onset gaps, tail).

Owner review (2026-10-17): boring -> more balls, ball sounds only -> paint_reveal2.

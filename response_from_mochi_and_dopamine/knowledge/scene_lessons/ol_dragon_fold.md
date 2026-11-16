# ol_dragon_fold (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md). It answers research/fractal_shorts.md #4 (Rollody's paper-fold dragon, 1.22M views) with our own look, HUD, music and payoff. It does not copy that video's colours, caption or "SHARED EDGES" label.
- Caption (baked, `--cap`; `--cap ''` = base): `Fold a strip ^in half^, again and again|until it becomes a ~DRAGON~`. `^x^` = the newest half's hue; `~x~` = gold.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_dragon_fold.mp4` (**v2**, Full HD, label fhd2, 13.65 s, 819 frames). No 4K yet.

## Versions
- v1 (15.35 s): folds 2-5 on the beats (0.43-2.16 s), the open over 2 beats (2.16-3.32 s), camera zoom-in 47.5 → 85 px/unit, no ghost. Reproduce with `--b0 12.25 --k5 85 --ghost 0`; the fold beats `B_F = 12, 13, 14, 15, 16`, `FOLD_W 0.92` and the open at beats 16-18 are constants in the code.
- Coordinator review of v1 (2026-10-23): "the middle and the 4-dragon finale look excellent; the first ~2 s are weak (at 1 s a small pink stack in a mostly black frame). Show the GOAL from frame 0 as a faint ghost, make the folding strip big and bright, bloom by ~1.6-1.8 s." → **v2**. The middle, finale, music sync, counters, colours and loop are kept; only the opening changed.
- v2 changes:
  - Folds 2-5 land on the eighths (the bass arpeggio) at 0.17 / 0.46 / 0.75 / 1.04 s.
  - Every crease opens 180° → 90° in 1 beat (1.04-1.62 s), so a real dragon is on screen from ~1.25 s.
  - The camera zooms in harder while folding (47.5 → ~140 px/unit), so the pile stays big: a striped tower with layers 0.058 units apart and a ribbon up to 36 px.
  - The GHOST appears (see World).
  - Frame 0 = score beat 15.2, so everything after the open moves 1.70 s earlier.

## World (logical 1080x1920)
- Content box: x 118-898, y 350-1128 (centre 508, 739). Black background, no arena line: the strip itself is the subject.
- **Ghost goal (v2):** the finished order-12 dragon, drawn exactly where the real one lands at fold 12 (the camera's framing at that moment), in its own gradient.
  - Alpha 0.22 from frame 0 through the open; it fades to 0.07 by fold 8, holds there, and fades to 0 in the 0.3 s after fold 12 lands.
  - The real dragon lands onto it.
  - It is cached once per canvas size.
- Act 1, physical folds: a 32-segment strip. Each fold flips the right half up and over onto the left, about the crease. Flipped layers stack in reverse order, so the outermost layer wraps the whole pile.
  - Pseudo-3D: lift = distance from the crease × sin(phi) × 0.30.
  - Folds 2-5 land on beats 15.5, 16, 16.5 and 17; each fold moves for 0.46 beat.
- The open: from fold 5, all 31 creases turn 180° → 90° together over 1 beat. The ease is 1-(1-u)^2.6 (they spring open), and the layer offsets fade out.
- Act 2, folds 6-12: the curve swings a copy of itself 90° about its end, one per 2 beats on beats 1 and 3. The copy starts hidden under the curve, so it peels out.
  - Corners are chamfered (0.24 units) once the curve is open.
  - Segments: 32 → 4,096 (true count, ×2 per fold).
- Colour: ONE ordered hue walk that never turns back, S 0.75, V 0.96.
  - The strip's 32 segments run rose-red (h .995) → pink → magenta → violet (.80) along the strip.
  - Each later fold's new half takes the next step: .76 / .72 / .68 / .635 / .585 / .53 / .47 (indigo → blue → azure → aqua).
  - The ramp ends at aqua: no coral and no mint (Mochi & Bolt colours).
  - Gold is the single accent: the meter goal (a tiny gold dragon icon + "DRAGON"), the "HEIGHWAY DRAGON" name, the crease/hinge glints and the lock ring.
- Payoff:
  - At fold 12 (9.69 s), "HEIGHWAY DRAGON" pops in gold.
  - 3 copies fan out together about the start point to 90°, 180° and 270°, landing on the cadence (10.85 s). They lock into a 4-fold rainbow mandala: warm centre, aqua arms.
  - Copies 1 and 3 are drawn at 0.80 brightness, so the four read as a pinwheel.
  - On the lock: a gold ring and a centre dot, plus "4 DRAGONS · ZERO OVERLAP". report() verifies 16,384 lattice edges, 0 shared.
  - During the hold, a calm band-by-band brightness ripple (+20%).
- HUD:
  - Meter: y 1262, 12 ticks, gold dragon goal shown from frame 0.
  - Counters: "FOLDS n / 12" (x 290) and "SEGMENTS 2ⁿ" with the true number (x 726), at y 1484.
  - "×2" pill in the newest hue, popping per fold.
  - Name lines: y 1194 and 1232.
  - Watermark: "DOPAMINE.EXE" (900 right, 1338), 35%.

## Camera
- Act 1: exponential zoom-in on the folding pile, K 47.5 → 140 px/unit (target at fold 5). Frame 0 = a ~760 px strip.
- From the open the camera only zooms out (a monotone envelope after the peak, ~104 px/unit at 1 s). The framing follows each swing: the fit is interpolated from the landed shape to the target. Settings: look-ahead 0.3 s, zoom smoothing σ 0.25 s, centre σ 0.45 s. Zoom-out runs ~0.4-0.5 ln/s.
- Finale: one smootherstep glide (score beats 32.1 → 33.6) to the 4-dragon framing (k 5.2), centred on the shared point.
- No rotation, no pulsing. The one zoom reversal is at the open (~1.1 s).
- Centre glide:
  - 130-160 px/s in Act 2, 250-370 px/s in the finale glide.
  - In the first second (up to 935 px/s) it is the pile re-centring while it folds.
- Worst overflow past the content box: 33 px, mid-fan (the spinning copies only).

## Timeline (clip s, 104 bpm, frame 0 = score beat 15.2)
- 0.00: the long strip (fold 1 done), its right half mid-flip; the ghost dragon behind. FOLDS 1/12, SEGMENTS 2.
- Fold landings: 2 → 0.17 s, 3 → 0.46, 4 → 0.75, 5 → 1.04, then 6 → 2.77, 7 → 3.92, 8 → 5.08, 9 → 6.23, 10 → 7.38, 11 → 8.54, 12 → 9.69.
- Open 1.04-1.62 s; lock / cadence 10.85 s; hold 2.2 s; 0.6 s dissolve into the pre-roll. Total 13.65 s.
- Folds landing per second: 3, 1, 1, 1, 0, 1, 1, 1, 1, 1 (+ the lock).
- Segments added per second: 14, 16, 32, 64, 0, 128, 256, 512, 1,024, 2,048.

## Sound
- **Music played as music** (owner rule 2026-10-23): Handel, "La Réjouissance", Music for the Royal Fireworks HWV 351 (1749; Handel d. 1759, PD).
  - Source: Mutopia "Mutopia-2013/09/01-1864" (trumpet in B-flat + organ, from IMSLP, Public Domain), saved at `<SOUNDFONTS_DIR>\scores\handel_rejouissance\LaRej.mid` with `SOURCE_mutopia_1864.txt`.
  - The trumpet track is written pitch; sounding = written − 2.
  - Not on the used/banned lists, not kid-coded. The channel's only earlier Handel is the Hallelujah (ol_spiral_maze).
- v2 excerpt: score beats 15.2-34, from the end of bar 3 (the held G; a note sounding at frame 0 is restarted at t = 0, then the high C at 0.17 s) to the F-major cadence on bar 8 beat 3. Played at one steady 104 bpm.
  - Folds 2-5 land on the bar-4 eighths of the bass walk.
- Arrangement (lib/orchestra):
  - Melody: oboe + violin + piano.
  - Organ right hand on strings (+ piano); horns double the melody an octave down from the open; trumpet joins (≤ G5) from score beat 24.
  - Organ left hand on cello, bassoon and contrabass (8vb).
  - Timpani B-flat2 / F2 on the bass note at score beats 16, 20, 24, 28 and 32 (folds 3, 6, 8, 10, 12).
  - Harp "rising tones": a 6-note run up the chord during the open, and 3 notes climbing on the eighths of every swing.
  - Cadence: held F major (strings, horns, oboe F5, soft trumpet, oohs, cello/contrabass F, timpani F2), a rolled piano chord, and a harp + celesta cascade. No boom.
- SFX: a soft paper crease per fold, with a 12 ms paper "tk" (band 1.2-4.2 kHz), a tonal partial on a chord tone that climbs with the fold, and a soft body. One also lands on the open, and a deeper one on the lock. There are 13 in all, ×0.30.
- `level_bed` (fin_db 6, cresc 3 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (v2, encoded Full HD = the delivered file)
- h264 yuv420p 1080x1920, 60 fps, 819 frames, 13.65 s.
- **flash_check PASS** (0 flashes, mean lum 0.015).
- **−14.00 LUFS**, peak −4.65 dBFS, last 0.5 s digital silence, energy > 5 kHz 0.05%.
- RMS per second: −19.3, −18.8, −19.5, −18.3, −19.0, −17.9, −17.9, −17.6, −17.5, −17.2, −16.9, −14.0 (cadence), −17.1, silence.
- Each crease tick sits within 0-8 ms of a detected onset.
- Seam:
  - Pre-encode, last → 0 = 0.84, against a normal 0 → 1 step of 0.90: the loop is exact.
  - Encoded, check_clip reads 1.10, against normal steps of 0.92 at the start and 0.75 at the end. The extra is x264 (frame 0 is a keyframe after a P-frame), during the fast opening motion.
- Frames read from the mp4 at 0, 0.5, 1, 1.5, 2, 9.75, 11.5 s and the last frame.
- v1 checks (same audio chain): flash PASS, −14.00 LUFS, seam 0.502 (normal step 0.508).

## Flags
- `--label --cap --still --frame a,b --dry --sound 0 --sfx (0.30) --fin (2.0) --bpm (104) --b0 (15.2) --hold (2.2)`.
- Camera: `--k5 (140) --la (0.3) --zsig (0.25) --csig (0.45) --follow (1) --fang0 (32.1) --fang1 (33.6)`.
- Look: `--sat (0.75) --copyv (0.80) --ghost (0.22)`.
- `--dry` prints the timeline, the per-second rates, the shared-edge check, camera speeds and zoom, and the overflow.

## Doubts for review
- The pace halves after the open: folds 2-5 land every eighth (0.29 s), folds 6-12 every 2 beats (1.15 s). The whole outline still changes on every swing, and the count of new segments per second keeps doubling.
- The zoom reverses once (in hard while folding, out from the bloom at ~1.1 s).
- The ghost overlaps the growing real dragon at low alpha during Act 2.

Owner review (2026-10-23): "I do not even know what I am looking at" -> shelved to DopamineExe/reserve (fails the 2-second readability test).

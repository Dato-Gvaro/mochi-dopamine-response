# chladni_plate3: Handel's Sarabande draws the sand (every chord = a new figure, on the beat)

- **Why it exists:** rework of chladni_plate2.
  - Owner review (2026-10-10): "we need a different song, and it must be in sync with the shapes; in this one, song and shapes seem out of touch."
  - v2 is untouched; this is a new file.
- **SYNC METHOD (the point):** one clock, `tq(q)` (score quarter → seconds), drives the music AND the sand.
  - Figure changes are no longer physics that drift near a note. Each one is a choreographed hop:
    - All 60,000 grains leave the plate on the chord's PICKUP (the quarter before: "da-DAAA"), spread over 70 ms.
    - They fly a parabola (height 0.15-0.30, perspective + defocus in the air), Hilbert-rank matched to a pre-settled grain set of the new figure.
    - Every grain lands on the chord's onset frame. Lock frame vs musical onset: within ±8.3 ms (frame quantisation).
  - The counter (+1), the landing glint and the colour hand-over complete on that same frame.
  - Between chords the sand dances on its figure with the music: each onset kicks the plate excitation, which drives the jitter.
  - **Timpani = plate jolt:** every timpani hit (TIMP list, the same list the audio renders) shakes the plate image (≤10 px, a 9 Hz decaying wobble) and lights its rim. A hit that is not a landing also bounces the sand bed (a 0.2 s hop).
  - The roll under the trill is a growing tremor. The trill itself boils the sand off its lines.
  - Audio attack vs lock frame (onset detection on the bed): +3 to +30 ms on 9 of 11 locks.
    - Lock 6: +83 ms (the horns' rise peaks after the timpani).
    - Final chord: +77 ms (the crash and boom bloom).
  - Visual timing uses frame-quantised lock times (LOCK_T). Using the musical times left the counter one frame late on the final chord (found in stills, fixed).
- **Figure complexity follows the orchestra:**
  - Bars 9-12 (thin: strings + choir + basses): (1,3)- | (2,4)+ | (3,5)+.
  - Bar 13, where the full orchestra enters with a boom and a cymbal swell: (4,6)+ | (5,7)+ | (4,8)- | (5,9)+ | (6,10)+ | (7,11)+.
  - The A7 climax with the trill: (8,12)- + 0.6 (4,14)-.
  - The final D minor: (10,14)- + 0.6 (6,16)-, which is also frame 0.
  - Each lock is 93-100 % on-line (<5 px) on landing. The A7 is boiled to 61 % by the trill on purpose.
- **Chord → figure map** (q = quarters from bar 9; minim = 64):

  | lock | chord | onset (s) | jump starts on |
  |---|---|---|---|
  | 0 | Dm (frame 0, already formed) | 0.000 | (none) |
  | 1 | A | 2.812 | E-G pickup |
  | 2 | F | 5.625 | bass G |
  | 3 | C | 8.438 | G-Bb pickup |
  | 4 | Gm | 11.250 | the D/A chord |
  | 5 | C7/E | 12.188 | bass G |
  | 6 | F | 14.062 | C pickup |
  | 7 | Bb | 15.938 | Dm |
  | 8 | Gm | 16.875 | C# |
  | 9 | Dm/A | 17.859 | E |
  | 10 | A7 + trill | 18.909 | beat-fraction before |
  | 11 | Dm | 20.638 | the leap from 19.50 |

  - Same-harmony beats (bar 9 beat 2, the bass walks) are timpani jolts and sand bounces, not new figures.
- **Hook:** frame 0 = figure 11, the finest: a rainbow lattice with a diagonal X, 60,000 grains, bright, the plate 0.89 of the width.
  - The opening D-minor tutti (boom + timpani) fires on frame 0, and the plate jolts within 2 frames.
  - The beat-2 timpani (0.94 s) jolts and bounces it again.
  - The first pickup (2.35 s) throws it into the simplest figure, and the build climbs back to it.
- **Engagement:**
  - Caption: "Every chord draws a new shape | ~Can 60,000 grains KEEP UP?~". Counter: "SHAPES: n/11" (11/11 gold at frame 0, 0 on the first jump).
  - Mochi and Bolt take turns bowing, and the turn passes on each pickup.
    - Her figures glow warm, his cool. Both bow the climax (rainbow).
    - Grin, wow and annoyed-stare reactions as in v2.
- **Twist:** the trill on the dominant boils the sand, and the timpani roll throws it off the plate ("TOO HARD!", Bolt stares at the camera).
  - A perspective fountain rises; the centre launches first, staggered over 19.50-20.00 s.
  - It rains down and locks as the finest figure exactly on the final D minor (boom + crash + cymbal swell peak). The counter goes gold at 11/11.
- **Loop:** exact.
  - The final landing targets ARE frame 0's grains (Hilbert permutation; sparkle weights follow it). The last 0.5 s holds them at rest.
  - The jolt and glows are 0 at frame 0 and at the end. The rim rises over ~2 frames. Character tilt uses the backward bow velocity.
- **Music:** G.F. Handel, Sarabande from the Keyboard Suite in D minor, HWV 437 (Handel d. 1759: the composition is public domain).
  - Notes: bars 9-16 of the theme. These open exactly like bars 1-4 (the famous opening) and close on the D-minor cadence.
  - Copied from Pierre Gouin's edition MIDI on IMSLP (#365930, Les Editions Outremontaises, CC BY-SA 4.0 for the file; the notes themselves are Handel's), with the two doubled organ manuals merged.
  - Cross-checked against P.A. Jones's engraving (IMSLP #103850, CC BY 3.0); the harmony and bass match. Bar 15's ornament is Gouin's realisation (trill F5-E5 on the A7, turn to D).
  - The beat-2 chords are played as the score's dotted halves (the MIDI articulates them as minims).
  - Tempo: minim = 64 (firm, sarabande stress on beats 1 and 2). Ritardando through bar 15 (×1.05 → ×1.25); the D before the last chord is held 0.85 s (the leap's flight).
  - **Arrangement** (ours, `lib/orchestra.py`, MuseScore_General MIT soundfont):
    - The opening chord is a tutti hit (boom, horns, tuba).
    - Bars 9-12: strings on the chords, horns on the melody, cello + contrabass + sub octave, choir "aah" pads.
    - Bar 13 on: + trombones (chords 8vb), tuba, trumpet and oohs on the melody 8vb, choir to full.
    - Timpani on the TIMP list (pitched to the bass). Booms on bar 9, bar 13 and the final chord.
    - A cymbal swell into bar 13 and another into the final chord. Timpani roll under the trill. Violins on the trill.
    - Range: highest note F5 (the trill), melody in C4-F5, bass down to D1 (sub).
- **Args:** --seed (5), --grains (60000), --tempo (64, minim), --k, --jit, --j0, --jt, --gain, --gw, --fresh-gain, --label, --cap, --still --frame a,b,c [--warm 40], --report, --fresh, --silent (no audio), --chunk a,b (one chunk, warmed 60 frames), --mux-only (re-mux an existing _silent.mp4).
  - The landing targets are cached in output/ (`_targets_<key>.npz`, ~3 min) and the sim too (`_sim_<key>.npz`, keyed on the sim parameters plus SIM_REV, ~1.5 min). Audio-only edits do not invalidate them.
- **Checks** (encoded Full HD, v1, seed 5):
  - Format: h264 yuv420p 1080x1920 at 60 fps, 24.48 s (1469 frames).
  - Audio: -14.01 LUFS, peak -5.05 dBFS, last 0.5 s at -84 dBFS.
  - RMS per second: hit -14 → phrase 1 at -19 to -22 → phrase 2 at -14 to -15 → final chord → silent.
  - flash_check: 0 flashes = PASS (mean luminance 0.026).
  - Loop:
    - Pre-encode seam (frame 0 vs frame 1468, half-res stills): 0.0 mean, 0.0 max = exact.
    - check_clip encoded seam: 0.637 (good band). The last frames are static (1467→1468: 0.001).
    - The frame 0→1 step is large (9.1 RGB mean) BY DESIGN: the opening timpani jolts the plate ~6 px.
  - Encoded frames read:
    - Hook: 0, 0.25, 0.5, 1, 2 and 3 s.
    - Locks: the onset frame and the 1-6 frames before it, at 2.82, 5.63, 11.25, 12.18, 15.93, 16.87, 17.87, 18.92 and 20.63 s.
    - The leap at 19.75 and 20.25 s.
    - Every figure is formed and the counter ticks ON the onset frame.
  - Seam bugs found in stills and fixed:
    - The rim-light was at full level on frame 0.
    - The character tilt used a forward bow velocity.
- **Render:** 10 chunks of 150 frames in 3 workers, each warmed 60 frames, then concatenated with `-c copy` and muxed via `--mux-only`.
  - ~1.7 s per frame per worker, ~25 min.
  - The driver is a scratchpad script (cp3_chunks.py). `NF_SCALE=1.0 python scenes/chladni_plate3.py --label v1` reproduces it sequentially.
- **Doubts:**
  - The frame-0 figure holds for 2.35 s before the first jump. The score has no chord change before the bar-10 pickup, so the hook rests on the opening tutti and two plate jolts (0.0 and 0.94 s), not on a collapse at 0.5-1 s.
  - The flight eases out, so the figure is ~97 % assembled 1-2 frames before the onset. The impact (glint, jolt, counter, colour) is ON the onset frame.
  - Bars 9-16, not 1-8. They open identically, but the first strain's half cadence on A is not heard. 16 bars do not fit in 30 s at a sarabande tempo.
  - The bar-15 ornament (trill F5-E5, turn to D) is Gouin's editorial realisation.
  - Strings swell slowly (121 ms t50). The onsets are carried by the timpani, brass and booms.
- Delivered <VIDEOS_DIR>\batch25\chladni_plate3.mp4 (Full HD). Owner review: pending.
- Owner review (2026-10-11): the point is that the sand REACTS to the sound; here it rearranges by itself with no smooth transition, not driven by the music -> chladni_plate4.
- Owner review (2026-10-11): rejected the mechanic. "The whole point of the sand and sound is how the sand REACTS to the sound... the sand rearranges by itself, there is no smooth transition, and it does it by itself, not by the music."
  - Lesson: choreographed hops onto pre-settled targets read as self-driven, even when they are frame-exact to the music.
  - The sand must be pushed by the audio itself, continuously. → chladni_plate4.

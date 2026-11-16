# fastest_slide: the brachistochrone race (Shortest path vs Fastest path), Verdi "Dies irae"

- **Brief:** coordinator task 2026-10-11 (batch26). The owner asked for "3 new videos with an initial hook, something FAMILIAR". The CORE FORMAT RULE applies: Mochi's choice vs Bolt's choice, the same physics judges both, one wins, and the clip shows WHY.
- **Geometry:** start A = (85, 575) and finish B = A + (pi*r, 2r), with r = 286.5 px (logical 1080x1920). The cycloid through A and B therefore ends at its lowest point. Every track shares A and B.
- **Physics:** exact. Frictionless beads start from rest. Each one integrates s'' = g * dy/ds along its own polyline (1600 samples, RK4, dt = 1/4800 s). g = 9.81 and r = 1.431 m, so the cycloid takes pi*sqrt(r/g) = 1.2000 s; the integrator matches to within 1e-6 s.
- **Tautochrone check:** beads released from 7 heights all arrive at 1.2000 s (spread < 1e-5 s).

## Rounds

Length is relative to the straight ramp (1.00). Each round's time is the true physics time; the HUD never shows display time.

| round | Mochi's choice | length | time | Bolt (cycloid, length 1.07) | margin | ghost beads |
|---|---|---|---|---|---|---|
| R1 | STRAIGHT ramp ("SHORTEST") | 1.00 | 1.42 s | 1.20 s | 0.22 s | none |
| R2 | PARABOLA | 1.03 | 1.25 s | 1.20 s | 0.05 s | straight 1.42, TOO DEEP 1.28 (length 1.30) |
| R3 | CIRCLE ARC (Galileo's guess) | 1.19 | 1.23 s | 1.20 s | 0.03 s | straight, parabola, too deep |
| R4 | HEAD START: halfway down Bolt's own curve (theta = 1.6) | 0.75 | 1.20 s | 1.20 s | **TIE** | none |
| R5 | 7 beads from 7 heights on a 7-lane cycloid ribbon | | all 1.20 s | | land together | none |

- **Why the cycloid wins:**
  - It drops vertically first, so its bead is fast EARLY (the live m/s bars on the cards).
  - Every bead reaches the same final speed of 7.5 m/s, because they all fall the same height.
  - The circle arc is the LONGEST path (1.19) and still comes second.
- **Mochi gets closer each round but never wins.** Laps under the cards read: Mochi 1.42 / 1.25 / 1.23 / 1.20, Bolt 1.20 every time.
- **Slow-mo** (rate shown as "SLOW-MO ×0.25 / ×0.2 / ×0.33"):
  - R2: tau 1.0-1.3.
  - R3: tau 0.9-1.3, which is 2 s of photo finish.
  - R5 landing: tau 0.6-1.2.

## Timeline

Display seconds. tb(beat) is the beat map below.

| time | event | music |
|---|---|---|
| 0.00 | payoff (frame 0) | hammer chord |
| 0.00-0.82 | REWIND | |
| 0.82 | R1 start | hammer |
| 2.02 | Bolt finishes R1 | hammer |
| 2.24 | Mochi finishes R1 | bell |
| 3.22 | R2 start | hammer |
| 5.02 | Bolt finishes R2 | big chord + boom |
| 6.22 | arc draws in, "GALILEO'S GUESS: A CIRCLE" | choir enters |
| 7.42 | R3 start | boom |
| 9.82 | Bolt finishes R3 | full choir + boom, after the timpani roll + cymbal swell |
| 11.02 | "HEAD START?" | |
| 12.22 | R4 start | boom |
| 13.42 | TIE | boom |
| 14.62-16.62 | 6 beads pop in, one per onset | choir triplet onsets |
| 17.02 | R5 release | boom |
| 19.42 | all 7 land | cadence chord + bells G-D-G |
| 19.42-23.32 | hold, the bed fades out (silent from 21.82) | |

- **Clip:** 23.32 s (1399 frames).
- **Finishes per 5 s:** 6 / 5 / 2 / 7. The end climbs back up to the 7-bead landing.

## Hook and loop

- **Frame 0 is the end state:**
  - Seven rainbow beads stacked on the finish line.
  - Their long-exposure streaks converge along the glowing 7-lane cycloid.
  - All ghost tracks are visible, with the banner "ALL TOGETHER! 1.20 s".
- **Rewind:** the hammer chord hits on frame 0. The beads run back up the slide (0-0.45 s), then morph into the race-1 setup with scanlines and "◀◀ REWIND". Race 1 starts at 0.82 s and the first finish is at 2.02 s.
- **Seam:** the clip ends on a static hold of exactly the frame-0 picture.
  - The characters hold their end pose for the last 1.6 s and the first 0.45 s.
  - Pre-encode seam: 0.000 mean / 0 max. Encoded: 0.451 (good band).

## Look

- Dark navy-violet stage with a faint lab grid and a soft stage light.
- Neon tracks drawn in 3 passes.
  - Mochi's current track is coral and Bolt's cycloid is mint.
  - The ghost tracks are muted: warm-white straight, gold parabola, sky arc, magenta too-deep.
- Beads have comet trails (the last 0.22 sim-s of their own path). In R5 the trails become persistent long-exposure streaks.
- R4/R5 turn the cycloid into a wide 7-lane ribbon. Lanes are offset 21 px along the curve normal; the physics stays on the centre-line cycloid.
- The finish gate has a laser line, posts and a chequered flag.
  - The timing flash is LOCAL (radial, r 150 px).
  - A time stamp pops above the gate on each winning finish.
- Track labels are rotated along their curve: "SHORTEST: 1.00" / "LONGER: 1.07" (R1), "PARABOLA 1.03", "CIRCLE 1.19", "TOO DEEP".
- **Cards** (y 300-505): name, choice, length, a big time in gold for the winner, and a live speed bar with m/s.
- **Characters** (r 46):
  - Mochi stands at (150, 1300) and Bolt at (835, 1305).
  - Mochi: wow → annoyed, worried during the photo finishes, a cheer on her head start, wow at the tie, and an annoyed stare at the end.
  - Bolt: cheers and a "HA HA" laugh after R1 and R3.
- **Safe zone:** content ends at y ≈ 1350 (0.70 h); the caption sits at 0.082 h.

## Music

- **Piece:** Verdi, Messa da Requiem (1874), "Dies irae", bars 1-9. Verdi died in 1901, so the work is public domain.
- **Notes:** the `lib/orchestra_pieces` "verdi_dies_irae" arrangement and score data (lib/scores/verdi_dies_irae.json). The source is the github.com/tuomas2/verdi-requiem vocal-score MusicXML; only the pitches and rhythms of the PD work are used.
- **Instruments:** MuseScore_General soundfont (MIT), via FluidSynth.
- **Retimed by a beat map:**
  - The four opening hammer chords fall at 0.02 / 0.82 / 2.02 / 3.22 s, with beat 8 at 5.02 s.
  - After that, quarter = 100 bpm.
- **Our additions:**
  - Booms on beats 12, 20 and 28 (race starts) and a lighter boom on beats 8 and 22.
  - Tubular bells (G minor tones) on every bead crossing the gate.
- **Measured onsets in the muxed mp4:** every race start and Bolt finish lands within 3 ms of its beat.

## Checks (encoded Full HD v1)

- **Video:** h264 yuv420p 1080x1920 60 fps, 1399 frames = 23.32 s.
- **Audio:**
  - Loudness: -14.01 LUFS, peak -5.26 dBFS.
  - Tail: T-1.3..T-0.5 peak -49 dBFS, last 0.5 s -84 dBFS.
- **flash_check:** 0 flashes = PASS (mean luminance 0.0135).
- **Frames read:** 0 / 0.25 / 0.5 / 1 / 2 / 3 / 5.1 / 9.9 / 13.42 / 16.3 / 18.5 / 19.45 / 23.3 s, plus a 1:1 crop of the gate at the landing, where all 7 beads sit exactly on the line.

## Args and delivery

- **Args:** `--cap "line1|~line2~"` (default "Shortest path vs Fastest path|~First ball down WINS~"), `--label`, `--still --frame N`, `--report`, `--audio-only`.
- **Delivered:** <VIDEOS_DIR>\batch26\fastest_slide.mp4 (Full HD).
- **v2 (2026-10-11, coordinator fix):**
  - Every pop banner now starts at 0.8x, overshoots to 1.15x by 0.07 s and settles by 0.14 s. Sizes are 62-90 px logical, so each banner reads from its first frame.
  - Long banners are split onto 2 lines.
  - The SLOW-MO tag moved down to y 925.
  - The video was re-rendered; the audio was re-muxed unchanged.
  - Checks: -14.01 LUFS, flash_check 0, pre-encode seam 0.000, encoded seam 0.464.
- **Owner review:** pending.
- Owner review (2026-10-11): good, but replace the song with sound effects (ball rolling, pleasant ASMR) -> fastest_slide2.

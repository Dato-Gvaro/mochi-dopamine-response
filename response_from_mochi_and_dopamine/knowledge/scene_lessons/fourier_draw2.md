# fourier_draw2 — BELL DUEL: fewest spinning circles to ring a church bell wins

- Brief (coordinator, 2026-10-09), rework of fourier_draw. Owner on v1: "I don't like the music and it lacks hook and engagement. I don't like high-pitch notes; … pleasant music, or bass and an epic famous melody." Fix all three: payoff-first hook, a duel/stake, Rachmaninoff's C#-minor Prelude in the low register.
- Maths:
  - Target: one closed outline, a church bell (crown knob, dome, waist, flared lip + rim band, clapper ball on a 14 px stem), cairo mask → Moore trace from the bottom-centre pixel (clapper bottom) → σ 1.5 smoothing → 4,096 points by arc length → `np.fft.fft`.
  - Circles in frequency order (±1, ±2, …), same coefficients for both sides, same pen phase.
  - Reconstruction error, max/mean px: 3: 88/38 · 10: 35/12 · 20: 17/6.6 · 22: 15/4.8 · 30: 9.4/2.2 · 50: 4.7/1.0.
  - Contact sheet (measured): 6 egg · 8 bell blob · 10-12 spike · 14-20 bare clapper STICK · **22 = clapper ball first forms** · ~30 crown knob · 40-50 crisp. This sets the game rule.
- Rule (engagement): a bell rings only when its clapper BALL is drawn; the fewest circles to ring wins. Contrasting methods: Mochi +10 at a time (big jumps), Bolt +1 at a time (one per bell note).
- Timeline (quarter 65.5; 1 lap = 4 beats; every big chord = lap closure on the clapper = RING TEST, both bells swing):

  | Time (s) | Music | Event |
  |---|---|---|
  | 0 | A (triple octaves) | Payoff frame: both bells drawn, chains spinning, RANG! 30 / 22 |
  | 0-0.92 | A → G# | Cold open: pens whip back 1 lap (Hermite, velocity-matched), counts collapse 30/22 → 3/3 (log space) |
  | 1.83 | C#m fff (reprise bar 46) | Test 1: 3 / 3 thunk |
  | 5.50 | C#m | Test 2: Mochi 10 / Bolt 5 thunk |
  | 9.17 | C#m | Test 3: Mochi 20 (stick, no ball) thunk, annoyed / Bolt 7 thunk |
  | 12.83 | E fff | Test 4: **Mochi 30 DONG** (3 rings), cheers; Bolt 9 thunk, wow |
  | 16.50 | G#m fff | Test 5: Bolt 11 thunk, worried; Mochi laughs (HA) |
  | 16.9-23.9 | falling chords (ritardando) | Bolt +1 on 11 of the 15 chords: 11 → 22, the stick then the ball forms |
  | 24.33 | final C#m, held | **Bolt 22 DONG** (5 bigger rings, glow) → BOLT WINS! 22 < 30; Mochi wow → annoyed stare (held across the seam) |
  | 26.3-27.67 | silence | payoff holds = frame 0 |

  - Bolt's count steps: beats 4, 5, 8, 9, 12, 13, 16, 17 (bell notes) then run chords 19, 20, 21, 22, 22.5 … 25.5, so the step rate climbs to the end.
- Look: dark indigo + starfield, coral (Mochi) / mint (Bolt) pools. Light layer (cairo, ADD/LIGHTEN): faint fill of the drawn shape, a 1-lap glowing trace (13 px soft + 4.4 px core, hue sweep per side, brighter over the last 0.12 lap), epicycle rings, white arm chain, pen; 2-radius bloom + hue-preserving tone-map (fourier_draw's). Bells 0.87 of the width (x 45-1000), characters r 42 below, counters at 0.775h with method labels / RANG!.
- Music:
  - Sergei Rachmaninoff, Prelude in C-sharp minor, Op. 3 No. 2 (1892; Rachmaninoff d. 1943): public-domain composition (US: published 1893; EU: life + 70 expired 2014). Played by our own `audio.synth_piano`, no recording.
  - Score source: Mutopia Project, `RachmaninoffS/O3/rach-prelude-op3-no2` (.mid + .ly, maintainer Petro Kostandy; the typesetting is CC BY-SA 4.0, the notes of the PD work are copied, not the engraving). Parsed with mido; the used notes are embedded in the scene as `SRC` with source beat numbers.
  - Used: the opening A-G# pickup (triple octaves A1-A2-A3, ff) → spliced onto the C# downbeat of bar 46 "Tempo primo, fff pesante" (same harmony at the join) → bars 46-52: bell motif A-G#-C# in octaves over massive C#m chords ×3, C-B-E, E-D#-G#m, the falling eighth chords over the G# pedal, the C#m arrival (source beat 202) held as the final chord (fermata, rolled).
  - Register: the top staff of the reprise (an octave doubling of the LH chords, up to B6) is dropped; the low staff's 4-note chords drop their sub-bass third (E1 under C#m is mud on a synth) = root-fifth-octave. Range C#1-E5; nothing above E5.
  - Ritardando over beats 22-26 (55 → 69 frames per beat). All notes faded by T − 1.35 s.
- Loop: every quantity is a pure function of the frame; pre-encode frame 1660 vs frame 0 mean diff 0.0015 (max 2/255), a normal step is 0.29.
- Args: --cap, --label, --still --frame, --report.
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920, 60 fps, 1660 frames = 27.67 s.
  - Audio: -14.00 LUFS, peak -6.08 dBFS, last 0.5 s at -74.7 dBFS; 221 notes, MIDI 25-76; notes/5 s 48, 51, 54, 48, then 20 in the tail.
  - flash_check: 0 flashes = PASS (mean luminance 0.018).
  - Loop: pre-encode frame 1660 == frame 0 (mean 0.0015); encoded seam mean 0.653 (good band).
  - Encoded frames read at 0, 0.25, 0.5, 1, 2, 13.1 (Mochi's DONG), 24.6 s (Bolt's DONG) + frame 0 at 200 px: two glowing bells + caption + RANG! 30 / 22 read at thumbnail size.
  - Render ~95 min on a loaded PC (other builds running).
- Delivered `<VIDEOS_DIR>\batch23\fourier_draw2.mp4`. Owner review: pending.
- Owner review (2026-10-10): doesn't like the shapes; ABANDON this idea.

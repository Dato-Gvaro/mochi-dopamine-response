# fourier_draw — FOURIER DRAWING: spinning circles draw Mochi, then Bolt, to Ode to Joy

- Brief (coordinator, 2026-10-09): an epicycle chain computed by DFT of a closed outline; its tip traces a glowing rainbow line. Mochi's silhouette, then Bolt's. Circles escalate 3 → 10 → 50 → 200 without restarting the motion. Each drawing fills in and becomes the real character, who blinks and smiles. Counter "CIRCLES: N". Music: Ode to Joy on piano.
  - Mid-build owner update (2026-10-10): slow, calm music is "boring". Ode to Joy is played brisk and joyful, with a driving march left hand; the circles turn faster to match.
- Maths:
  - Target = the TRUE silhouette of `toon.draw_char` (alpha mask, holes filled), at r 350:
    - Mochi: body + ink rim + curl.
    - Bolt: rounded square + stem + leaves.
  - Each target is traced (Moore neighbour, from the bottom-centre pixel, clockwise on screen), smoothed σ 1 px, and resampled to 4,096 points by arc length.
  - Each target is then run through `np.fft.fft`: c_k = one circle, radius |c_k|, k turns per lap, centred on the previous circle's rim. The anchor is c_0 (the centroid).
  - Circles are taken in FREQUENCY order (±1, ±2, …). N circles = the N lowest frequencies, so the Mochi → Bolt morph interpolates matching coefficients.
  - Reconstruction error, max/mean in px:

    | Character | 3 | 10 | 50 | 100 | 200 |
    |---|---|---|---|---|---|
    | Mochi | 137/48 | 71/17 | 11/1.3 | 4.4/0.25 | 1.9/0.07 |
    | Bolt | 113/44 | 76/29 | 13/1.1 | 5.5/0.32 | 2.6/0.13 |

  - Mochi at 50 still had a lumpy curl, so the 100 step was moved BEFORE her reveal.
- The drawn line is the CURRENT partial sum over [tail, head]. When circles fade in (smoothstep weights on a continuous N_eff), the whole curve morphs toward the true shape and the motion never restarts.
- Timeline:
  - The clock is 1 lap = 190 frames = 8 beats (quarter = 151.6). The tip phase is (f + 44.5)/190, so every phrase-end note (beats 14, 30, 46, 62) is a lap closure, with a soft ring at the closure point.

  | Time (s) | Music | Event |
  |---|---|---|
  | 0 | — | 3 circles; Mochi blob, trace already 0.23 lap in |
  | 3.22 | bar 3 | 10 circles |
  | 6.38 | bar 5 | 50 circles |
  | 9.55 | bar 7 | 100 circles |
  | 11.93 | bar 8, D cadence | Mochi floods in from the closure point (0.55 s), eyes open, blinks, happy grin; she melts back into the line at +1.75 s |
  | 13.9-15.9 | — | The line morphs into Bolt at 100 circles (soft stem and leaves) |
  | 19.05 | bar 13, the A' recap | 200 circles |
  | 24.59 | final D cadence | Bolt floods in: eyes open, "wow", blink, grin |
  | 26.4-28.5 | — | Bolt melts, circles retract 200 → 3, coefficients morph back to Mochi's, trace un-draws to frame 0's exact state |

  - During each reveal the epicycles dim to 28 %.
- Look:
  - Dark indigo stage + starfield. The light layer is cairo:
    - thin violet epicycle rings (ADD);
    - a bright white arm chain with joint dots;
    - a rainbow ribbon drawn opaque with LIGHTEN (hue fixed by curve phase; round caps would bead under ADD/OVER), 13 px soft + 4.6 px core, brighter over the last 0.1 lap;
    - a white-hot pen.
  - The light layer gets a 2-radius gaussian bloom and a hue-preserving tone-map.
- Music:
  - Beethoven, Symphony No. 9 in D minor, Op. 125, finale, "Ode to Joy" theme (premiered 1824; Beethoven d. 1827): public-domain composition, played by our own `audio.synth_piano`, so no recording is used.
  - Full 16-bar theme A A' B A' in D major, in the standard simplified form (no bar-12 syncopation).
  - Melody F#5–A5 (low A4 at the B cadence).
  - March left hand:
    - bass on beats 1 and 3 (root, or the fifth when the chord holds);
    - an octave doubling every 2nd downbeat;
    - staccato triads on beats 2 and 4.
  - Harmony per half bar:
    - A: D D | A7 A7 | D D | D A
    - A': … | A D
    - B: A D | A D | A Bm | E A
  - Steady tempo (no accelerando, no ritardando). Ends on the tonic D with a rolled, held D chord.
  - All notes are faded out by T − 1.35 s.
- Args: --cap, --label, --still --frame, --report.
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920, 60 fps, 1710 frames = 28.50 s. Render ~27 min on a loaded PC.
  - Audio: -14.00 LUFS, peak -5.68 dBFS, last 0.5 s at -240 dBFS (soundtrack -57 dB at T-1.5 s).
  - 200 notes. Events per 5 s: 46, 43, 49, 43, then 19 in the tail.
  - flash_check: 0 = PASS (mean luminance 0.017).
  - Loop: pre-encode, frame 1710 == frame 0 exactly (diff 0.0); a normal step is 0.53. Encoded seam 0.642.
- Delivered `<VIDEOS_DIR>\batch22\fourier_draw.mp4`. Owner review: pending.
- Owner review (2026-10-09): music disliked; lacks hook and engagement; no high-pitched notes; wants pleasant, or bass + epic famous melody -> fourier_draw2.

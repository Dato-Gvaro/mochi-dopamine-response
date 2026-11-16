# pendulum_wave — the pendulum wave, 10 -> 20 -> 40

- First clip of the "brain-satisfying maths/physics" direction (BRIEF 2026-10-08). A top view in 9:16. The row runs down the frame and every bob swings left-right across a centre spine (its thread is a spoke from the spine). Mochi rides the longest (slowest) pendulum at the top; Bolt rides the shortest (fastest) one at the bottom.
- Law: pendulum k makes (K + k) full swings in the cycle Tc. Its length is L_k = g (T_k / 2pi)^2 with T_k = Tc/(K+k), and its motion is x = A cos(sqrt(g/L_k) t) (the exact small-angle solution). Every pendulum is released from the same board. The realignment error at Tc is 0.0 (float).
- Rounds (no seed; the clip is deterministic):

  | Round | N | K | Tc | Swings | Freq | L | Group labels |
  |---|---|---|---|---|---|---|---|
  | 1 | 10 | 4 | 4 s | 4..13 | 1.00-3.25 Hz | 24.8-2.35 cm | 2 |
  | 2 | 20 | 6 | 6 s | 6..25 | 1.00-4.17 Hz | 24.8-1.43 cm | 2, 3 |
  | 3 | 40 | 10 | 10 s | 10..49 | 1.00-4.90 Hz | 24.8-1.03 cm | 2, 3, 4 |

- Each round: a gold release bar retracts at the start. Playback eases into slow motion over the last 0.62 sim-s before Tc (0.30x at the realignment; playback only, the physics is untouched). The bar returns and catches the line at Tc: "IN SYNC!", ripples, a happy hop.
  - Mid holds last 0.56 s: the row re-spaces and new bobs grow in between, and the counter bumps.
  - Catches at 4.51 / 11.57 / 22.64 s. Clip 24.73 s (1484 frames).
- Order overlay: thin curves join every q-th bob while the bobs form q smooth waves (coherence of q*t/Tc to an integer). This makes the hidden 2/3/4-group order visible. A label "q GROUPS" shows at each p/q moment, and their number grows per round (1 -> 3 -> 5).
- Faces: normal at release; "wow" at group moments and on the slow-mo approach; dizzy (X eyes, orbiting stars, wobble) when no q <= Q is coherent; Bolt sweats in round 3; happy grin at every catch.
- Sound (bed, built in the scene):
  - Every centre pass is a candidate marimba note (D major pentatonic; long = low, short = high). There are 3150 passes in all.
  - Passes within 18 ms merge into a chord (up to 4 notes). The rate cap is 78/64/54 ms by round, and the bigger (more in-sync) chords win the slots. The result is 240 chords, about 9/s -> 11/s -> 13-15/s.
  - Blue Danube (PD Strauss, our synth, glassharp +12) walks one note per group moment and per catch. Each catch adds a wood/brass TOCK and a chord under the melody note (D, then G, then D).
  - A soft tock plays at each release (audio at frame 0). Everything fades by the last catch + 0.8 s.
  - The sidecar events are note_gain 0, so regen_audio cannot rebuild the bed.
- Loop: after the last catch the 30 extra bobs shrink into the 10 kept slots (silent), and the counter goes back to 10. The last frame equals frame 0 (bar in, 10 bobs at +A, normal faces). Pre-encode seam 0.041 (normal step 1.14).
- Checks (encoded Full HD): h264 yuv420p 1080x1920 60 fps, 24.73 s. -14.00 LUFS, peak -7.42 dBFS, last 0.5 s -62.0 dBFS. Encoded seam 0.267. flash_check: 0 flashes = PASS (mean lum 0.016).
- Args: --cap ("a|~b~"), --melody (blue_danube), --label, --no-lines (no group curves), --audio-only, --still --frame.
- Delivered <VIDEOS_DIR>\batch19\pendulum_wave.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-09: Start at 40 and move WAY slower to enjoy the visuals; continuous background music -> pendulum_wave2.

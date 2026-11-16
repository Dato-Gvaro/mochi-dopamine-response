# spirograph — 1 -> 60 gears in one ring, true hypotrochoids, Rondo alla Turca on piano

- Brief: coordinator task 2026-10-09 (batch22). Brain-satisfying maths, BRIEF_brain.md (energy update 2026-10-10 applied: lively tempo).
- Maths: ring pitch radius R = 450 px. A gear of radius r rolls inside it; a pen hole at d from the gear centre traces
  x = (R-r) cos t + d cos((R-r)/r t), y = (R-r) sin t - d sin((R-r)/r t).
  - R/r = p/q in lowest terms: p-fold symmetry, closes after exactly q trips round the ring (t = 2 pi q).
  - The gear's drawn rotation is the rolling angle -(R-r)/r t; ring 150 teeth, gear teeth 150 q/p (rounded), meshing at the contact point.
  - A formation of n copies rotated by 2 pi j/n with gcd(n, p) = 1 is the finest interleave 2 pi/(p n) of the curve, so its gears ride evenly spaced round the ring (no gear overlap except 8:3, ~8 px).
- Escalation (one continuous run, nothing restarts). Each formation starts on a downbeat and closes 4 bars later on a phrase downbeat:

  | Pens | ring:gear | d/r | start | close | rev/s |
  |---|---|---|---|---|---|
  | 1 (flower) | 5:3 | 0.55 | 0.00 s | 3.27 s (first C6) | 0.92 |
  | +4 = 5 | 7:2 | 0.85 | 3.27 | 6.95 (half cadence E) | 0.54 |
  | +5 = 10 | 8:3 | 0.60 | 6.95 | 10.63 | 0.82 |
  | +5 = 15 | 6:1 | 0.95 | 8.79 | 12.47 | 0.27 |
  | +5 = 20 | 3:1 | 0.90 | 10.63 | 14.31 | 0.27 |
  | +8 = 28 | 11:3 | 0.90 | 12.47 | 16.15 | 0.82 |
  | +10 = 38 | 9:2 | 0.70 | 14.31 | 17.99 (C6 of the return) | 0.54 |
  | +10 = 48 | 13:3 | 0.60 | 16.15 | 19.83 | 0.82 |
  | +12 = 60 | 5:1 | 0.90 | 17.99 | 21.87 (final A cadence) | 0.26 |

  - Closures per phrase climb 1, 4, 5, 5, 5, 8, 10, 10, 12. Counter "PENS: N" (pop on each formation); small label "ring : gear = p : q" of the newest formation.
- Look: float light buffer, bilinear splat of every pen's ink (precomputed per pen, so any frame renders statelessly).
  - Fresh ink is hot (x3.2), cooling over 0.3 s. Finished curves fade gently to 60 % (the hero flower to 78 %).
  - Closing glow 0.7 per formation; a 0.3 bloom of the whole mandala on the cadence.
  - Bloom sigma 1.4 / 5 px; hue-preserving tone-map; dark violet stage; steel ring with inner teeth.
  - Gears are translucent with toothed rims, spiral holes and a white-hot pen hole. Non-hero gears at 80 % (newest formation) / 40 % (older); gears fade 0.15-0.9 s after their curve closes.
  - Small sparks in the pen colour on each close. Mochi and Bolt (r 30) sit on a ledge at the lower left, eyes on the newest pens: wow at the first close and at 60, happy from the cadence.
- Loop: the cadence is followed by a 1.0 s hold, then the mandala dissolves newest-first over 2.0 s (counter 60 -> 1, label steps back to 5:3). Gear 1 rolls back in, pen up, over the last 1.1 s, arriving at its frame-0 spot with its frame-0 speed.
- Music: Mozart, Piano Sonata No. 11 in A major K. 331, 3rd mvt "Rondo alla Turca" (1783; Mozart d. 1791) — public domain.
  - Notes are taken verbatim from the Mutopia Project's public-domain edition (KV331_3_RondoAllaTurca, MIDI parsed), bars 1-24 (pickup to the A cadence): the A-minor theme, the C-major strain, and the theme's return. The repeats are not taken.
  - Played by our own `audio.synth_piano` (bed, no recording). Allegretto quarter = 130 (0.46 s), driving damped left-hand 8ths, bar-downbeat accents. Grace notes G5-A5 before the B5s in bars 5-7. Ritardando +0.05 (x-45)^2 s over the last bar.
  - Everything is faded out by T-1.40 s.
- Args: --q (0.46 s per quarter), --cap, --label, --still --frame N, --report.
- Look tuning (render 2): ink 0.55 -> 0.68; gear dimming added because 5 big 3:1 gears read as busy at 12 s.
- Loop: T_END is snapped to the frame grid (frame nf == frame 0). Pre-encode seam 0.723 = a normal step (frame 0->1: 0.723). The encoded seam is 1.26 (check_clip 1.145), inside the encoder's normal end-of-stream alternation of 0.88/1.27 between consecutive frames. Frame 0->1 encoded is 0.90; gear 1 is big and moving on both sides of the seam.
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920, 60 fps, 25.03 s (1502 frames). Render ~20 min.
  - Audio: -14.01 LUFS, peak -6.5 dBFS, last 0.5 s silent (-240 dBFS). Events/5 s 68/62/51/61/23 (steady music, no rush).
  - flash_check: 0 flashes, PASS (mean luminance 0.010).
- Delivered <VIDEOS_DIR>\batch22\spirograph.mp4. Owner review: pending.
- Owner review (2026-10-09): music disliked; not pleasant to watch. Dropped.

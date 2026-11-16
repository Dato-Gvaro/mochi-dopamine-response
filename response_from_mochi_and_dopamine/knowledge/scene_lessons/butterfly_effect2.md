# butterfly_effect2 — 100 -> 1,000 -> 5,000 double pendulums, slow motion

- Built from the owner's review of butterfly_effect (2026-10-09). The asks:
  - start with 100, go to 1000 or more;
  - move SLOWER, as eye candy;
  - space-y classical music, violin.

  butterfly_effect.py is untouched; this file is standalone.
- Physics: the real double-pendulum equations, RK4 at a fixed dt of 1/480 s. Energy drift is ≤ 1e-8.
  - The slow motion is honest: g/L = 16 x 0.36^2 = 2.07. This is exactly v1's dynamics played at 0.36x, because the equations are time-scale invariant in g.
  - Neighbours differ by 0.001° in theta1.
- Ladder:

  | N | Release θ1 / θ2 | Run | Bloom (spread > 25 px) |
  |---|---|---|---|
  | 100 | 135° / 60°, LAUNCHED at w = (+1.5, -1.5) rad/s | 8.4 s | 3.38 s |
  | 1,000 | -170° / -90°, from rest | 7.0 s | 2.77 s |
  | 5,000 | 160° / 150°, from rest | 6.6 s | 0.87 s |

  - The 100 is launched so that frame 0 is already moving. A from-rest release from a high pose sat still for ~1 s in slow motion.
  - Morph between releases 1.2 s; collapse 2.6 s; clip 27.0 s (1620 frames).
- Look: a float light buffer, not cairo strokes.
  - Every arm is sampled every ~1 px and splatted additively: bilinear up to 1,000 arms, nearest pixel for the 5,000.
  - Per-arm intensity: 100 = 0.30, 1,000 = 0.075, 5,000 = 0.014. The tips get a bead.
  - Trails: the buffer decays 0.95/frame and shows at 0.07 under the live arms. For N ≤ 1,000 the trail gets sub-frame samples (4 / 2 per frame) so a sweep is smooth, not a strobe.
  - Glow: 1/2-res sigma 1.5 (weight 0.55) plus 1/4-res sigma 5 (weight 0.35).
  - Tone-map: 75 % hue-preserving and 25 % per-channel `1-exp(-1.25x)`, so dense regions stay coloured rather than white. With per-channel only, the 5,000 blew out to white.
  - Background: starfield (260 stars, seeded) on a plum radial gradient. Camera breath zoom ≤ 1.05 per run.
  - Render time ~25 min at Full HD (numpy splat, ~0.7-1 s/frame).
- Mochi and Bolt (r 27) ride arm 0 and the last arm, gazing at the pivot. Moods are awe only: smile -> wow at the bloom -> alternating happy / wow. Never dizzy.
- Collapse: an exponential pull (k 4.5; k 6 for the morphs) plus the arms' own momentum, ending on the next release's launch velocity (Hermite h11). The arm is therefore already moving at the seam.
  - The trail buffer blends into frame 0's steady state (`warm0 = layer0 / (1 - 0.95)`) over the last 0.55 s.
  - Pre-encode seam: mean delta 0.205, the same as a normal step (0.199 / 0.219).
- Sound: `lib/bgm.py` Gymnopédie No. 1 (Satie, PD) on a violin section + pad accompaniment, gain 0.8, start_beat 9. On top: a soft chime triad at each count-up (D-A / F#-D, in key), a two-note sparkle at each bloom, and a falling D-major chime at the collapse. The bgm tail is exact zeros for the last 1.3 s.
- Args: --cap, --label, --piece (gymnopedie_1), --voice (violin), --bgm-gain (0.8), --start-beat (9), --still --frame [--warm 150].
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920 60 fps, 27.00 s.
  - Audio: -14.00 LUFS, peak -4.6 dBFS, last 0.5 s -71 dBFS (below -48 from T-1.0 s). The first 0.25 s is -24.5 dBFS peak (bgm 0.5 s fade-in).
  - flash_check: 0 flashes = PASS. Encoded seam 0.343.
- Delivered <VIDEOS_DIR>\batch20\butterfly_effect2.mp4. Owner review: pending.
- Owner review 2026-10-09: Overall good, but the music is bad; and each count-up restarts the motion, which breaks the smooth flow -> butterfly_effect3 (continuous).

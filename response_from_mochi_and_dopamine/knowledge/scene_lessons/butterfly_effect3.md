# butterfly_effect3 — one continuous 5,000-pendulum release, Moonlight Sonata on piano

- Built from the owner's review of butterfly_effect2 (2026-10-09):
  - "the music sucks";
  - "when you switch to more you break the smooth movement and run to start" — wanted one continuous motion and familiar classical music.

  v2 stays bit-reproducible; v3 imports only v2's pure helpers (bg, blit, down2/up2, grad, stage constants).
- Physics: ONE ensemble of 5,000 double pendulums, theta1 0.001° apart (total 5°).
  - Real equations, RK4 at a fixed dt of 1/480 s, slow-motion gravity g/L = 16 x 0.33^2.
  - Launched at frame 0 from (165°, 30°) with w = (-1, +1) rad/s. Energy drift ~1e-8.
  - Pose chosen by a 150-pose search: bloom by ~2 s, theta2 phase coherence R < 0.3 only at ~18 s, so the fan -> ribbons -> orb arc spans the whole run. The first pick (135°, 60°) became a uniform orb by 8 s.
- Reveal (no restarts):
  - Bar 1: every 50th arm is drawn (100 arms, label "difference: 0.05°").
  - Bar 2 downbeat: the every-5th set fades in over 1.6 s (1,000, "0.005°").
  - Bar 3 downbeat: all arms (5,000, "0.001°").
  - The label is the TRUE neighbour spacing of what is on screen. Caption: "5,000 pendulums, 0.001° apart | ~Watch CHAOS bloom~".
  - Per-arm intensity is 0.30 x (100 / n)^0.6, so the fan gets brighter but never blows out.
- Look: v2's float light buffer (splat, trails 0.95/frame at 0.07, sub-frame trail samples while < 2,000 arms, 2-radius glow, hue-preserving tone-map, starfield). One camera breath over the run (zoom ≤ 1.05). Mochi and Bolt (r 27) ride arms 0 and 4950, in awe.
- Loop:
  - At the cadence (+0.25 s) a 3.4 s exponential pull (k 4.5) plus the arms' own momentum lands on the launch velocity (Hermite h11), so the arm is moving at the seam.
  - The extra arms fade out while gathering and the counter steps 5,000 -> 1,000 -> 100.
  - Trails blend into frame 0's steady state over the last 0.6 s.
  - Pre-encode seam: mean delta 0.096, a normal step being 0.10-0.22.
- Music: Beethoven, Piano Sonata No. 14 in C# minor "Moonlight", Op. 27 No. 2, 1st movement (published 1802; Beethoven d. 1827) — public domain. Played by our own `audio.synth_piano` (direct call: NoteBank clamps below C2). No recording, no bed, no chimes.
  - Bars 1-4 + the bar-5 downbeat ONLY. Bar 5's melody entry was left out: the passage is not certain enough note-for-note.
  - Real rhythm: 4 triplet-eighth groups per bar, octave bass on the bar / half bar.

    | Bar | Harmony | RH triplets | LH octave |
    |---|---|---|---|
    | 1 | C#m | G#3 C#4 E4 | C#2/C#3 |
    | 2 | C#m/B | same | B1/B2 |
    | 3 | A, then D/F# | A3 C#4 E4 x2, A3 D4 F#4 x2 | A1/A2, then F#1/F#2 |
    | 4 | G#7 | G#3 B#3 F#4, G#3 C#4 E4, G#3 C#4 D#4, F#3 B#3 D#4 | G#1/G#2 |
    | 5 (downbeat) | C#m cadence | lightly rolled, held | — |

  - Adagio quarter = 46, with a ritardando over the last 2 beats of bar 4. Gentle per-bar swell. Every note gets a release fade; all of it is faded out 1.35 s before the end (silent seam).
  - The count-ups land on the bar 2 and bar 3 downbeats; the collapse starts on the cadence.
- Args: --pose th1,th2,w1,w2 (165,30,-1,1), --slow (0.33), --cap, --label, --still --frame [--warm 150], --report.
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920 60 fps, 25.02 s (1501 frames). Render ~25 min.
  - Audio: -14.00 LUFS, peak -2.3 dBFS (the opening bass octave), last 0.5 s -90 dBFS (below -56 from T-1.25 s).
  - flash_check: 0 flashes = PASS. Encoded seam 0.344.
- Delivered <VIDEOS_DIR>\batch21\butterfly_effect3.mp4. Owner review: pending.
- Owner review 2026-10-10: good visuals, but the characters riding the arms are distracting; seat them at the bottom -> butterfly_effect4 (4K -> Oct 13 slot 1).

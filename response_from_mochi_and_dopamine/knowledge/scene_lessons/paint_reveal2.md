# paint_reveal2
- paint_reveal rebuilt after the owner's review (2026-10-17): "boooring — we need more balls, ball sound only". `scenes/paint_reveal2.py` is a NEW file; paint_reveal stays bit-reproducible. Pure mechanic, no characters.
- Caption: `Every bounce paints ^ONE^ pixel|~Until the masterpiece appears~`. One readout: `PAINTED n%` -> `ONLY n LEFT` -> `PAINTED 100%`. The painting is never named on screen.

## Image
- Same source and crop as paint_reveal (Wikimedia Commons `File:Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg`, {{PD-Art|PD-old-100-expired}}; see docs/scenes/paint_reveal.md).
- The grid is now finer: **108 x 100 tiles of 9 px (10,800)**. Asset: `assets/paint_reveal/starry_night_108x100.png`, built with `--build-grid <jpg>` (LANCZOS). Same grading. The finer grid makes the swirls read from mid-clip.

## Physics (numpy; all balls in one step)
- **The tile rule is unchanged.** An unpainted tile is solid: the ball reflects off it and paints exactly that tile (the deepest contact). Painted tiles are open space.
- **New: ball-ball collisions.** Equal-mass elastic collisions; pairs per substep come from `scipy.spatial.cKDTree.query_pairs(2R)`, with overlap separation. Collisions are the second sound source.
- **Balls:** R 4. They start at 760 px/s (collisions then spread the speeds).
- **Step and record:** substep 1/300 s, positions recorded at 120/s.
- **Start:** 9 patches = 2904 tiles (26.9%). **64 balls** are spread inside the patches. The pre-roll is 0.5 physics s, so frame 0 is 29.2% painted, with paints from frame 0.
- **Splits:** EVERY ball splits at 1700 / 3300 / 4900 / 6300 painted: **64 -> 128 -> 256 -> 512 -> 1024**. A child spawns 1.15 R to the side, so new pairs don't explode.
- **Pacing:** mild 0.5x on the last tile only.

| Event (seed 1) | Clip s |
|---|---|
| splits ->128/256/512/1024 | 3.71 / 6.47 / 8.53 / 10.16 |
| 50% / 90% painted | 5.01 / 10.85 |
| 10 left / 3 left / 1 left | 17.32 / 17.47 / 17.75 |
| last tile (1, 99) | 18.47 |
| clip end | 22.37 |

- Painted % at 0/1/2/3 s: 29.2 / 33.3 / 37.0 / 40.4.
- Paints per 2 s: 846 788 1150 1502 1646 1060 432 161 62 1. Ball-ball hits per 2 s: 209 → ~20,000 once there are 1024 balls (128k in total).
- **Rendering:**
  - Layers (dark ghost / painted / smooth), plus a per-tile A8 mask.
  - Balls are one pre-rendered sprite each (glow, bright core, thin dark rim), with all motion streaks in a single stroke.
  - x264 is held to `-threads 2` (an own Writer subclass), in one process.
- **Finale:** as in paint_reveal: rings, ball bursts, the tiles melting into the bicubic image, zoom out to 0.94, a gold rim and 14 twinkles. Then a 0.6 s dissolve into the pre-roll.

## Sound: ball sounds ONLY (no melody, chords, pads or beds)
- **Grains:** raw contacts (paints + ball hits) merge into grains. A grain absorbs every contact closer than its gap: 12 ms plus 0-10 ms of seeded jitter, so the rain never locks into a periodic buzz.
- **Grain sound:** a paint tik (last_brick2 recipe; f0 1000-1330 Hz by tile brightness, fuller when merged) and/or a dry glassy ball click (f0 1350-1750 Hz, 2 ms decay).
- **Level:** density-aware, g = 0.55 (1 + rate/25)^-0.5.
- **Other sounds:**
  - A soft bubble pop per split.
  - A bigger pop on the last pixel: 150 -> 520 Hz, a 105 Hz thump and a 4-tik sprinkle.
  - A glass sparkle shower for the bursting balls, thinned to >= 45 ms over 1.8 s, plus 28 twinkle pings. All on random G5-E6 pitches: clean tones, not a tune.
- **Counts:** 1145 events (1096 grains: 817 tik+click, 248 click-only, 31 tik-only). That is ~52 grains/s from frame 0 to the hunt. Min gap 12.0 ms.
- **Master:** `audio.master(reverb 0.25, peak_db -6)`, last 1.0 s digital silence.

## Checks (encoded Full HD, seed 1)
- h264 yuv420p 1080x1920, 60 fps, 1342 frames = **22.37 s**.
- -14.03 LUFS, peak -7.31 dBFS. The last sound is at 21.37 s, then silence. Energy above 3 kHz: 0.96%.
- flash_check PASS: 0 flashes (mean luminance 0.039).
- Seam: pre-encode last -> 0 mean delta 0.749 vs a normal step of 0.768 (exact). Encoded 2.14 (a swarm-busy I-frame).
- **Encoded frames:** read at 0, 0.5, 1, 2, 3, 9, 17.5, 18.6 and 20.5 s, plus a 1:1 crop at 9 s. The balls read as bright dots with a dark rim, even on the light sky. At 9 s (77%) the swirl is unmistakable. The 20.5 s frame shows the smooth painting with its gold rim.
- Safe zone: as paint_reveal (frame bottom 0.664 h).
- Delivered `<VIDEOS_DIR>\batch41\paint_reveal2.mp4`. Owner review: pending.

## Flags
`--seed --label --cap --still --frame N --dry --sound 0 --peak`; physics `--balls --v --splits`; `--build-grid <jpg>`.

## Doubts
- **Falling paint rate:** paints peak at 6-10 s and then fall (the open picture leaves few targets). The grain rate holds ~52/s to the end because ball clicks take over. The ear hears a steady rain, the eye a growing swarm.
- **Very short hunt:** 10 left -> done in 1.15 s.
- **1024 balls:** the end swarm is dense (owner taste: "not heavy/crowded" vs "more balls"); 512 would be calmer.
- **Unheard:** I have not listened; I checked by numbers only.

Owner review (2026-10-18): dropped.

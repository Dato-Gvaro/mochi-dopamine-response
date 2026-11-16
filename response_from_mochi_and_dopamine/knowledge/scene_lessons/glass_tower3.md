# glass_tower3
- Rework of glass_tower2 after the owner review (2026-10-17): "remove a row or two from the bottom; instead of starting with the first glass full, start with empty; put our characters on top making them pour those balls — two colours — and the challenge is which colour's balls STAY more in the glasses". glass_tower2.py is untouched; its ball engine is copied (not imported).
- Caption (baked, `--cap`): `Every glass must ^FILL^|~Most balls INSIDE wins~`. The question form "Whose balls STAY…?" was a viewer prediction, so it is not used.
- HUD: one cluster under the tower.
  - `GLASSES FULL n/10` becomes a gold `· k LEFT` for the last 2, then `MOCHI WINS` / `BOLT WINS` in the winner's colour.
  - Below it is the lead bar with the live ball counts (coral left, mint right). The divider moves by margin / max(30, 8% of the balls), so it shows the lead, not a pie.

## World (logical px)
- 10 coupes in rows 1-4: rim width 152, pitch 215 (63 px gaps = 7 ball diameters), bowl 66 deep, rows 200 apart. Top rim y 552, floor y 1352 (0.704 h). The tower spans x 72-868.
- Glasses are neutral crystal. A full glass glows in the colour of its majority of balls.
- Mochi (x 300) and Bolt (x 640) stand on glass ledges at y ≈ 466, r 46. Each tips a bucket: coral from the mouth at (424, 476), mint from (516, 476), each thrown toward the centre at 70 px/s into the top glass.
- Balls: r 4.5, 3 shades per colour.

## Physics (glass_tower2 engine)
- Position-based dynamics, 6 substeps. Gravity 2400, terminal speed 1250.
- cKDTree contacts: inelastic (restitution 0.08), pairwise friction 0.3.
- Two-sided thin bowl walls. The frame edges are walls, so the spill stays on the floor. Stems and feet are visual only.
- **Both buckets pour exactly the same schedule:** Q = 32·exp(0.03 t + 0.003 t²) balls/s each, from 0.2 s before frame 0. Who leads is pure cascade chaos: which lip a heap spills over, balls knocked out.
- **Full rule:** a glass is full when its bowl holds ≥ 84 balls for 6 frames.
- **Score:** the balls of each colour inside bowls, frozen at the moment of 10/10.
- **Lead change:** needs a margin of 8 balls (`LEAD_HYST`).
- **`--search N`:** seeds 1-8 were tried (at Q0 32). s6 was chosen for its story:
  - BOLT leads early.
  - 9.7 s: MOCHI takes the lead.
  - 13.4 s: BOLT retakes it.
  - 13.9 s: MOCHI again.
  - **Final: CORAL 559 vs MINT 535, MOCHI wins.**
- **Fills (s6):** top 1.28 · row 2 5.6/5.9 · row 3 11.0-11.3 · row 4 16.18-16.35 s. The bottom row fills almost together, so 2 LEFT / 1 LEFT lasts only ~0.15 s.
- **Frame 0:** the tower is empty but moving. Both streams are in the air, and the first balls land at about 0.1 s.
- **Reactions** (toon.watcher_pose):
  - A lead change makes the new leader laugh (0.7 s) and the other worried (0.9 s).
  - Otherwise the leader is happy and the trailer determined.
  - Finish: the winner gives 5 cheer hops; the loser gives an annoyed stare.
- **Finale:**
  - The buckets tip back up and the pour stops over 0.3 s.
  - A band of light rises with sparkles in the winner's colour, and a soft glow sits behind the tower.
  - Zoom 1.0 → 0.94 → 1.0.
  - At last glass + 3.4 s, a 0.6 s dissolve runs into the pre-roll (empty tower, buckets tipping).
- Clip 20.43 s (1226 frames).

## Sound: ASMR only (owner 2026-10-17: "we don't need a melody here, but a more pleasant ASMR sound of balls dropping")
- The first version's Vivaldi tings, harp, strings and E-major cadence are all removed. The functions are still in the file, unused.
- **Contact samples:** the sim records the contacts above 50 px/s per frame, up to 24 per kind, each with its kind, x and speed (`sim["snd"]`).
  - The samples use their own RNG, so the physics is bit-identical to the first render: all ball positions were checked equal.
  - The picture was not re-rendered. The new audio is remuxed onto the same video stream (`--audio-only`, stream copy, no `-shortest`).
- **Clusters:** one cluster event per frame, holding 1-7 clicks (more when more balls touch).
  - Clicks are chosen by speed, spread over 15 ms, and panned by x (±0.9 across the tower).
  - Gain ∝ (v/vmax)^0.6 / √m, and the frame's level is capped at (E/E85)^0.32. Dense moments merge into a smooth "rain of marbles" instead of getting louder.
- **Click bank** (40 variants per kind, rounded 0.4 ms attack, no noise):
  - Ball on ball: a small dry tik, 0.95-1.4 kHz, 2-3.4 ms.
  - Ball on glass: a soft resonant bowl tink, 1.15-1.5 kHz, 28-50 ms ring, very soft.
  - Floor: a deeper tok, 380-560 Hz.
  - Bucket lip: a soft 0.7-0.95 kHz tick.
  - Settling piles give the low-speed contacts: a quiet patter built from tiny clicks.
- **Glass FULL:** a soft clean glass ping, about 1 kHz (the same pitch every time, ±¼ semitone detune). It is not a melody note.
- **Finale:** the shower of settling clicks fades out (envelope to 0 at T − 1.0 s). The last 1.0 s is digital silence.
- **Numbers:** 1151 clusters and 6114 clicks; clicks per 5 s 1062 / 1551 / 1942 / 1559 (finale). Onsets are at least 12.0 ms apart. Energy above 3 kHz is 0.29%. L/R correlation is 0.89.
- `audio.master(reverb=0.30, peak_db=-6)`.

## Laptop
- One sim process (about 20 s per seed, cached in `output/glass_tower3_sim_<args>.pkl`; `--resim` reruns it).
- One render process. The encoder is capped at `-threads 2` by the scene's own `Writer2`; lib's VideoWriter has no thread cap.

## Checks (encoded Full HD, s6)
- h264 yuv420p 1080x1920, 60 fps, 1226 frames = 20.43 s.
- ASMR remux: -14.02 LUFS, peak -7.74 dBFS, the last 0.5 s digital silence. (The melody version measured -13.98 LUFS.)
- flash_check PASS (0 flashes).
- Seam:
  - Pre-encode, last → 0 is 0.114 against a normal step of 0.119 (perfect). The last frame vs pre-roll −1 differs by 0.058 (compositing).
  - Encoded seam 0.376.
- Encoded frames read at 0, 0.5, 1, 2, 3, 9.7, 16.35 and 18 s.
- Safe zone: the characters sit at x ≤ 686 (< 0.85 w), content ends at 0.70 h, the HUD sits at 0.73-0.77 h.

## Doubts
- 20.4 s is the low end of 20-30. A slower pour would stretch it, but the opening would get calmer.
- The bottom row fills within 0.2 s, so there is no last-glass suspense. The suspense is the lead race (the 13.4 s retake), not the last glass.
- The margin is small (24 of ~1100), and the lead bar exaggerates it (by design). The numbers are the honest score.

Delivered `<VIDEOS_DIR>\batch41\glass_tower3.mp4`. Owner review: pending.

Owner review (2026-10-17): "we don't need a melody here, more pleasant ASMR sound of balls dropping" -> sound-only rebuild (no melody).

Owner review (2026-10-18): approved -> 4K.

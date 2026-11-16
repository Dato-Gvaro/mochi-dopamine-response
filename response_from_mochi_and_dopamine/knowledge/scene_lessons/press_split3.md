# press_split3 — franchise episode of press_split2: every crushed ball splits into **4**

- **THE ONE CHANGE: every crushed ball splits into 4 (press_split2: 3).** Everything else is press_split2 (docs/scenes/press_split2.md): look, palette, machines, Mochi = press / Bolt = hammer, counters, Für Elise note-per-crush, banners, jam + plate snap + eruption finale, dissolve loop.
- Why: press_split2 went viral (2026-10-17, 38K views in <24 h, 77.6 % stayed). Episode built 2026-10-17 (batch41).
- Caption: "Every ball ~CRUSHED~ splits / into ~4~ SMALLER ones" (CRUSHED and 4 in gold) + "Press or Hammer: which OVERFLOWS first?". The line-2 stake is unchanged.
- Consequences of 4 children, and how they are handled:
  - Child radius 0.583× (was 0.66). Area grows ×1.36 per split (was ×1.31), so the press's 16,384 still fills to MAX. 8 generations: 100, 58, 34, 20, 11.6, 6.7, 3.9, 2.3 px. A ball under 3.0 px is dust (was 4.5), so gen 7 is the dust.
  - Press counts run exactly 1, 4, 16, 64, 256, 1,024, 4,096, 16,384. The overflow lands on the 7th wave, mid-way to 16,384.
  - CAP_N is 36,000 (the hammer reaches about 10.8k). split() is bounds-guarded.
  - Press period P_PER0 is 4.2 s (was 3.9). With one fewer wave needed, this keeps the finale at about 23 s.
  - Hammer budget E_K is 0.38 (was 0.34). The hammer has to stay ahead of 4,096 until the last wave and end close to MAX.
- Seed 3. Seeds 0-9 searched at E_K 0.34: the press wins every time, with the hammer 113-300 px under MAX. At E_K 0.38, seed 3 is the tightest.
  - Counts, press/hammer (sim time; clip time = sim − 0.6 s):

    | Sim time | Press | Hammer |
    |---|---|---|
    | 4 s | 16 | 205 |
    | 12 s | 256 | 3,898 |
    | 20 s | 4,096 | 7,756 |
    | 22 s | 5,899 | 9,364 |
    | 24 s | 16,384 | 10,831 |

  - The hammer leads from about 1 s. LEAD CHANGE at **21.7 s clip**, mid-way through the press's last wave.
  - PRESS OVERFLOWS at **22.8 s**, with the hammer pile 74 px under MAX at 10,198 balls. The plate snaps and the pile erupts at 23.2 s. The dissolve runs from 24.0 s.
  - Clip 24.62 s (1477 frames).
  - **Winner: PRESS (Mochi)**, the same outcome as press_split2.
- Hook: the first split is the hammer's at 0.17 s, the press's at 0.18 s. Both counters read 4 by 0.3 s.
- Render: `run_render_cool` is toon.run_render with x264 `-threads 2` (laptop-cool rule). The sim is pickled to `output/press_split3_s<seed>_sim.pkl` (`--fresh` re-simulates). Run with OMP/OPENBLAS threads = 1.
- Cost: sim about 5 min, single thread.
- Known nits (inherited): foamy piles with voids; a one-ball dust column on the hammer chamber's wall; the eruption covers the caption for the last second.
- Checks (encoded Full HD, seed 3, render ~10 min):
  - Video: h264 yuv420p 1080x1920 60 fps, 24.62 s, 106 MB.
  - Loudness: -13.98 LUFS, peak -4.9 dBFS.
  - Notes: 93 (one per crush, merged per 60 ms). Notes per 5 s: 14, 24, 24, 31 (climbing).
  - flash_check: 1 flash = PASS (worst 1 s = 1 at 22.77 s, the overflow). Mean luminance 0.048.
  - Seam mean delta 1.40 (press_split2: 1.39). Same reason: the dissolve plus a fast-falling hammer. The last frame is the frame before frame 0.
  - Tail: last 0.5 s peak -8 dBFS, last 100 ms -9 dB, the same as press_split2 (-10.6 dB). The bed fade (-26 dB raw) is lifted about 16 dB by master()'s loudness gain into the limiter, so the dissolve loop's tail is NOT silent. This is inherited; fix both episodes together if wanted (a steeper or earlier bed fade).
  - Encoded frames read at 0, 0.3, 1, 3, 12, 21.7 (LEAD CHANGE, 9,463 / 9,391), 22.83 (OVERFLOW, 16,384 / 10,198), 23.5 (PRESS WINS), 24.17 (dissolve) and 24.6 s (the last frame = the frame-0 state).
- Delivered <VIDEOS_DIR>\batch41\press_split3.mp4 (Full HD). Owner review: pending.

Owner review (2026-10-18): dropped.

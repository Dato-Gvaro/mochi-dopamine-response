# snake_duel5: snake_duel4 recut with a mid-action opening and a dissolve loop (2026-10-14)

- Why: owner rule 2026-10-13: rewind openings "do not look nice". Frame 0 must be MID-ACTION, and the clip loops by a dissolve (SCROLL-STOP RULES in docs/BRIEF_batch25.md).
- Same games (seed 447), ASMR soundscape (minus the rewind whoosh), story and game clock as snake_duel4.
- The clip is a window on the game timeline: clip time = game time - T_START, with T_START = 1.40 s (0.52 s after the game's GO).
  - Frame 0: both length-3 snakes are moving, and Mochi's gem is one cell ahead. Mochi's first gem is at ~0.1 s, Bolt's at ~0.2 s.
  - No rewind and no GO banner. "MOCHI LEADS!" at 2.15 s; TRAPPED at 11.09 s; BOLT PASSES at 15.11 s; PERFECT GAME at 20.17 s.
- Loop: the payoff holds HOLD = 1.1 s. Then a DIS = 0.5 s dissolve fades in the game's own half-second BEFORE frame 0, so picture and motion arrive exactly at frame 0.
  - The audio tail is cross-faded the same way (`clip_bed`), so there is no silent gap. The last 0.5 s peaks at -8.4 dBFS by design.
  - The encoded seam mean is 0.82 (4K) / 0.97 (FHD). That is a one-frame motion step of the moving snakes, not a jump.
- Checks: 1306 frames = 21.77 s, 60 fps, h264 yuv420p. FHD 1080x1920 and 4K 2160x3840 (label ship). -13.98 LUFS, peak -6.92 dBFS. flash_check PASS (0 flashes).
- Shipped: the 4K render REPLACED <VIDEOS_DIR>\Schedule\2026-10-15\2_snake_duel4.mp4 (filename kept).
- Doubt: frame 0 is mid-action but small (two 3-cell snakes on dark boards). The big rainbow payoff now arrives only at the end.

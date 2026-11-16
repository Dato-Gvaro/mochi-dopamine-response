# neon_trails5 — neon_trails4 with a mid-action opening (2026-10-14)

- **Why:** owner rule 2026-10-13: rewind/reverse openings "do not look nice". Frame 0 must be MID-ACTION, and the loop is a seamless dissolve (docs/BRIEF_batch25.md SCROLL-STOP RULES).
- **Unchanged from neon_trails4 (approved):** the game (seed 100056, 22x24, WALL HUGGER vs CUTTER), the music ("Night Drive 140", original) and the look.

## Timeline (clip = a window onto the game clock)
- Frame 0 = 0.6 s after GO (game time 1.35 s). Both bikes are racing and the CUTTER is zig-zagging, with turns every 1-2 steps on the 16ths.
- "CUT OFF! -354 cells" at clip 2.40 s.
- The drop at clip 2.08 s.
- The final crash on the last chord at clip 14.94 s.
- The payoff holds 1.0 s, then **dissolves over 0.5 s** into the race 0.5 s before frame 0. The last frame = game frame f_s - 1, so the loop is continuous.
- **Audio:** the same game-clock render, cut to the window. Its last 0.5 s crossfades into the music just before frame 0, so the audio loops as seamlessly as the picture. There is no silent tail, by design (the dissolve-loop rule).

## Checks (4K ship = <VIDEOS_DIR>\Schedule\2026-10-15\3_neon_trails4.mp4)
- h264 yuv420p 2160x3840, 60 fps, 986 frames = **16.43 s**.
- LUFS -13.96, peak -2.39 dBFS.
- flash_check: 0 flashes.
- **Seam:**
  - Pre-encode (Full HD) 985→0 = 0.434, equal to normal motion (0.45): seamless.
  - Post-encode 0.723 (4K) / 0.889 (Full HD): keyframe + fast motion, under the 1.1 "broken" line.
- Frames read at 0, 0.5 and 16 s.

## Doubt
- **Length 16.43 s,** under the 20-35 s band: the rewind (0.75 s) and the ring + silent tail (3.75 s) are gone. A longer clip needs a longer game (new seed) or a slower tempo, which would change the approved cut.

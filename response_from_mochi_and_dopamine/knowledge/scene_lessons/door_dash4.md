# door_dash4: door_dash3 with a finish-line progress track instead of the "n/12" counters

- Owner on door_dash3 (2026-10-06): "this will do too, but instead of them having score 12, maybe they go toward a FINISH LINE: just a line with the finish at the end, and as they progress it shows." door_dash3.py is untouched.
- This file IMPORTS door_dash3: its sim, director, race, camera, sound and all drawing. Only the bottom HUD is new. The race is identical: seed 42, Bolt wins at 14.22 s, Mochi 0.35 s later, clip 17.02 s (1021 frames).
- HUD (v2 of the strip, after the coordinator's "make it bold" note: the r 19 markers on a thin line were too small at phone size):
  - One bold track bar (18 px, dark core, lilac rim and glow) at y 1462, x 70 -> 900 (~0.77 w; the finish stays out of the right-edge strip). 12 faint level ticks.
  - A checkered finish strip across both lanes, plus a pole with a big waving checkered flag (92x62). Everything glows gold when the winner arrives.
  - Progress fills inside the bar: Mochi = coral upper half, Bolt = mint lower half, each with a soft glow behind it in its colour.
  - The markers ARE the characters: faces r 38 (Mochi rides 36 px above the bar, Bolt 36 px below), each with a halo in its own colour; the leader is drawn on top. v3's reactions (worried, wow, laugh, cheer, wince, annoyed) play on the markers, with jumps at 0.6x height.
  - The big characters are dropped, so the bottom 20% stays clear (the lowest pixel is y ~1536).
  - Position = CONTINUOUS depth progress (ball world y / shaft length), not level steps. The markers glide back to the start in the last 1.15-0.45 s (loop seam = frame 0).
- LEAD swaps come from the progress with 0.02 hysteresis: 4.05 s Bolt, 7.88 s Mochi, 11.90 s Bolt. On each, the new leader's marker flares (halo x1.4, face +12 %, 0.6 s) and a 62 px "LEAD!" in its colour pops above the track.
- Checks:
  - Full HD: h264 yuv420p 1080x1920 60 fps, -14.01 LUFS, peak -5.8 dBFS, last 0.5 s -84 dBFS, flash_check PASS.
  - 4K ship (`NF_SCALE=2.0 --label ship`, re-rendered with the bold strip): h264 yuv420p 2160x3840 60 fps, 1021 frames, -14.01 LUFS, peak -5.83 dBFS, last 0.5 s -84.3 dBFS. flash_check 0 = PASS. Seam 1.95 (continuous scroll).
- Args: --seed (42), --label, --cap, --melody, --voice, --still --frame.
- Delivered: Full HD <VIDEOS_DIR>\batch15\door_dash4.mp4. Shipped 4K: <VIDEOS_DIR>\Schedule\2026-10-10\2_door_dash.mp4 (owner approved the clip).
- Owner review 2026-10-07: Scheduled (Oct 10).

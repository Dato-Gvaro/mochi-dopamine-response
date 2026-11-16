# last_brick2
- This is last_brick plus spectators and ASMR sound, made after the owner's review of last_brick (2026-10-16): "ok — make our characters appear somewhere, and instead of music use a tik-tik ASMR sound of breaking".
- `scenes/last_brick2.py` is a COPY of last_brick (not an import), so both stay reproducible. The seed (9), physics, visuals, the mild 0.5x on the final hit, the finale and the loop are all unchanged. See docs/scenes/last_brick.md for the mechanic.

## Cast (spectators only, never in the physics)
- Mochi (x 168) and Bolt (x 852, left of the 0.85 w strip) sit on the box's top rail: r 34, feet at y 344, flanking the `BRICKS LEFT` readout.
- **Gaze:** they look at the mean of the breaks in the last 0.35 physics-s. During the hunt they look at the remaining last-10 bricks, then at the last brick. The gaze is smoothed per frame (k 0.25).
- **Reactions** (`toon.watcher_pose`; Bolt is 0.07 s behind Mochi):
  - `wow` (0.7 s) at each split.
  - `worried` from 10 left until the final brick (sweat, plus a lean of up to 0.16 rad toward the hunt).
  - `wince` on each near miss.
  - 3 × `cheer` hops from 100%.

## Sound: ASMR breaking only (no melody, chords or pads)
Modelled on sand_rise3 `s_tik` and block_tower2 `s_tick`.
- **tik** per brick break: 3 inharmonic modes (f0, 2.32 f0, 0.51 f0; 3.5-10 ms decays) plus a 2.5 ms click band-limited to 0.9-2.6 kHz.
  - f0 is 1050-1430 Hz, higher for higher bricks, ±7% random.
  - Breaks closer than 12 ms merge into one fuller tik, so dense runs become a crackling cascade.
  - Level is density-aware: g = 0.55·(1 + rate/25)^-0.45.
- **pop** per split: a 260 → 680 Hz bubble blip.
- **Final crack** on the last brick: a 720 Hz modal snap, a 4-tik shatter over 66 ms and a 115 Hz thump.
- **Tinkle shower:** one soft glass ping per bursting ball (thinned to ≥ 45 ms, at most 1.6 s), on C6-A6 pitches with random choice. These are single pings, not a melody.
- Every onset is ≥ 12 ms apart. `audio.master(reverb=0.25, peak_db=-6)` (impulses).
- Numbers: 686 sound events (656 tiks). Tiks per 2 s: 30 27 36 31 42 51 69 53 77 80 85 67 | 8 (the hunt). Energy above 3 kHz is 2.1%.

## Checks (Full HD, seed 9)
- h264 yuv420p 1080x1920, 60 fps, 1781 frames = **29.68 s**.
- -14.02 LUFS, peak -6.44 dBFS; the last 1.05 s is silent.
- flash_check PASS (1 flash: the dissolve).
- Seam: pre-encode last → 0 has a mean delta of 0.222 vs a normal step of 0.215, so it is exact. Encoded: 1.53 (I-frame).
- Stills read at 0, 13, 25.5 and 27 s: the faces read, the 25.5 s frame shows the worried look with sweat, and the 27 s frame shows the cheer. The cheer hop rises to y ~250, beside caption line 2, not over it.
- Delivered Full HD as `<VIDEOS_DIR>\batch38\last_brick2.mp4` (it replaced last_brick.mp4 there). The 4K is `output/last_brick2_ship_9x16.mp4`.

## Doubts
- The characters are small (r 34) by design; they read best in the cheer.
- The hunt (24-26 s) is quiet: only the 9 last tiks (RMS -26 dB vs -16 to -18 dB around it). That is tension by design, followed by the crack.

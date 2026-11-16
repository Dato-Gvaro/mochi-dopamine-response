# spiral_roll2
- This is a rework of spiral_roll after the owner review of 2026-10-16. The owner wanted ONE shooter that tries again and again and gets further each time, until EVERY brick is gone. spiral_roll.py is untouched.
- Caption (baked, `--cap`): `Every try breaks a little ^MORE^|~Until EVERY brick is gone~`.
- World:
  - The geometry is the same as spiral_roll, moved down 52 px: centre (520, 920), outer wall r = 468 − 96φ/2π, 3.5 turns, 420 radial bricks.
  - The bricks are one rainbow along the spiral: red at the mouth through to violet at the centre, HSV 0 → 0.8.
  - Broken bricks STAY broken, so the eaten spiral is the progress meter.
- Launcher: a spring barrel on the lead-in at the top-left (x 30-196, axis y 493), with a zigzag spring, a gold plunger and one gauge lamp per crank.
- Bolt sits on the barrel. Each reload:
  - A new Mochi drops into the barrel.
  - "POWER +10%" pops beside it.
  - Bolt hops and stomps, and the plunger snaps forward: thunk.
  - Bolt looks annoyed after each stall. He cheers in the finale cameo (bottom-left, x 168, y 1250).
- Readout pill (y 284-354): `TRY n` and `BRICKS LEFT n`. The count turns gold for the last 12 and at 0.

## Physics (honest, the same for every shot; v = V0·√E, V0 2500 px/s, 8 substeps)
- Shot n is launched with P = 1.10^(n−1). Bolt cranks it +10% per reload, and it is shown on screen.
- Rolling friction is 4e-5 per px everywhere.
- A brick costs 0.054 × (mid radius / 400).
  - Bricks are wedges, so inner bricks are smaller and cheaper. Per px of track, the brick cost is the same everywhere.
  - If E is below the next brick's cost, Mochi bounces off it, goes dizzy and pops 0.2 s later.
- The cleared path costs only friction, so every try reaches the frontier with most of its energy. That is why each try gets further.
- s7 (deterministic):

| Try | Power | Bricks broken | Total | Ends (clip s) |
|---|---|---|---|---|
| 1 | 1.00 | 17 | 17 | 0.21 |
| 2 | 1.10 | 19 | 36 | 1.33 |
| 3 | 1.21 | 22 | 58 | 2.69 |
| 4 | 1.33 | 25 | 83 | 4.18 |
| 5 | 1.46 | 29 | 112 | 5.85 |
| 6 | 1.61 | 34 | 146 | 7.68 |
| 7 | 1.77 | 41 | 187 | 9.69 |
| 8 | 1.95 | 51 | 238 | 11.86 |
| 9 | 2.14 | 70 | 308 | 14.36 |
| 10 | 2.36 | 112 | 420 | ALL CLEARED |

- On try 10, Mochi reaches the last brick with only E 0.131 of 2.36 to spare, so she barely makes it. `--ebk 0.054` was chosen for that; 0.056 would need an 11th try with a big surplus.
- The last 12 bricks run in slow motion: the clock runs at 0.062x, so 12 bricks take 1.15 s of clip, from 16.85 to 17.99 s.
  - The camera pushes in 2.2x on the centre.
  - The waiting bricks pulse white, and each one pops with its own rising note.
- Then she glides 0.32 s into the hub, ALL CLEARED! appears, and the finale follows:
  - The camera zooms on to 2.8x.
  - A soft gold glow builds, 7 rainbow rings bloom outward, and the walls take a gold halo.
  - Mochi is happy, and Bolt hops in cheering.
- A 0.6 s dissolve leads into the pre-roll, where Bolt stomps the first shot.
- Clip 21.75 s (1305 frames). Frame 0 is try 1, 0.26 s after the fire, already smashing the red bricks (410 left).

## Sound (all synthesized; no music, no beds, no whoosh/hiss)
- Brick ticks:
  - A struck bar (f, 2.76f, 4.07f) plus a soft click.
  - Notes walk the C-major pentatonic C4 → A5 inward, with a 0-2-1-3 arpeggio.
  - Ticks are thinned to one per 42 ms of clip time or more; the gain grows with the bricks merged into a tick.
- Rolling taps: a soft G3 tap at every 1/8 turn through the cleared path. They speed up as she spirals inward.
- The last 12 bricks get their own run notes C4 → E6 with a longer ring, at least 90 ms apart in slow motion.
- Launcher thunk: 150 → 82 Hz plus a 330 Hz wood knock, no noise. Also a hop tap, two crank clicks and a load tap.
- Stall: a low bonk, then a small rising pop when she vanishes.
- Finale: a rolled C-major chord with a low root swell, plus a G5 glass chime.
- Onsets are at least 12 ms apart, nothing in the last 1.0 s, `master(peak_db=-6)`. 0.1% of the energy is above 3 kHz.

## Flags
- `--seed --label --cap --vote` (a vote banner at y 1130 from reach + 1.0 s; default OFF) `--still --frame N --dry --sound 0`.
- Physics: `--v0 --pow --ebk --fr`.
- The sim raises an error if a try breaks nothing or the spiral is never cleared.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1305 frames = 21.75 s.
- −14.01 LUFS, peak −7.6 dBFS, last 0.5 s at −49 dBFS.
- flash_check PASS (0 flashes).
- Seam: pre-encode −1 → 0 is 0.45 against a step of 0.45 (−1 → 1 is 0.69), so the loop is perfect. Encoded seam 1.72 (I-frame).
- Events per 5 s: 51 / 60 / 61 / 43 (the last bin is slow-motion run plus finale). 215 sound events.
- Safe zone:
  - The caption is at y 172-245 and the readout at 284-354.
  - The world is clipped to y ≥ 368. The spiral ends at 1340 (0.70h). Bolt's cameo is at ≤ 1310.

Delivered <VIDEOS_DIR>\batch38\spiral_roll2.mp4. Owner review: pending.

## Fix (2026-10-16): no bullet time at the finish
The owner rule is "no slow motion at the finish", so the 0.062x bullet time is gone. The tables above describe v1; this section replaces them.
- **Bigger final bricks:** the last 12 bricks are 5 slots wide (15 deg), so the last half turn holds them. They are 30% lighter and white-outlined, and still pulse. The brick count is now 360 + 12 = 372.
- **Honest cost:** each brick still costs EB_K x (r/400) x (width/3 deg), so the cost per px of track is unchanged.
- **Retuned so the last try barely makes it:** `--ebk 0.0538 --fr 0.000046` was grid-searched so that try 10 clears the last brick with E 0.002 left. Her energy runs out naturally, so she slows into the final bricks.
- **The final bricks play at a mild 0.5x** (`--slow`). They pop at clip 17.00, 17.05, 17.09, 17.13, 17.18, 17.23, 17.28, 17.33, 17.39, 17.46, 17.55 and 17.66 s. The gaps grow from 41 to 113 ms, a natural slow-down, with one rising note each.
- **Camera:** the push-in is kept at 2.2x. The bricks stay ahead of Mochi on the inner half turn, so she never hides them.
- **Bricks per try:** 17 / 19 / 22 / 25 / 29 / 34 / 40 / 50 / 68 / 68.
- **Timing:** she reaches the hub at 18.49 s. Clip 21.70 s (1302 frames).
- **Checks:**
  - -14.01 LUFS, peak -7.3 dBFS, last 0.5 s at -47 dBFS.
  - flash_check PASS (0 flashes).
  - Pre-encode seam 0.43 against a step of 0.42 (perfect); encoded seam 1.80.
  - Events per 5 s: 52 / 60 / 69 / 27.

Owner review (2026-10-16): APPROVED. 4K render: `NF_SCALE=2.0 --label ship --ebk 0.0538 --fr 0.000046` -> output/spiral_roll2_ship_9x16.mp4 (h264 yuv420p 2160x3840, 60 fps, 1302 frames = 21.700 s, -14.01 LUFS, peak -7.25 dBFS, last 0.5 s at -46.7 dBFS, flash_check PASS 0). Left in output/ for the coordinator to stage.

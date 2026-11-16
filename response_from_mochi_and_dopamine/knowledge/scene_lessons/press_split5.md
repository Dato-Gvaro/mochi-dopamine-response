# press_split5 — press_split2 episode: CUBES

- **THE ONE CHANGE: "Every CUBE crushed splits into 3".** The balls are now glossy bevelled cubes, graded by generation the same way: Mochi's go crimson → orange → gold, Bolt's go blue → cyan → mint.
- Everything else is press_split2 (docs/scenes/press_split2.md): machines, timings, faces, counters, Für Elise note-per-crush, banners, overflow finale, the 0.6 s dissolve loop and the 0.6 s pre-roll. It is a new file; press_split2 is untouched.
- Caption (baked):
  - "Every ~CUBE~ crushed splits"
  - "into 3 ~SMALLER~ cubes"
  - "Press or Hammer: which OVERFLOWS first?"
- The counter reads "Cubes: N".
- Rule: a crushed cube becomes 3 cubes at 0.66× its side, so the area grows ×1.31 per split, as with the balls.
  - The first cube has a half-side of 95 px (`CUBE_K` 0.95 × the ball's R0; env `PS5_K`).
  - Generation 8 is dust and never splits.
- Cube physics (the honest consequences):
  - **Contacts:** axis-aligned box contacts that push along the axis of least overlap. The broad phase is a Chebyshev KD-tree (`p=inf`).
  - **No rolling:** a cube whose centre sits over its support hull keeps 0.72 of its horizontal velocity per substep (friction), so it does not roll.
  - **Tipping:** a cube whose centre overhangs its support slides off sideways (2600 px/s²) and tips (38 rad/s²).
  - **Drawn angle only:** fresh pieces spin (up to ±9 rad/s) while airborne and settle flat on landing. Collision stays axis-aligned.
  - **Piles:** the press pile stacks like bricks and the hammer pile has a steep left slope, with gaps and voids.
  - **The press wave can miss a cube:** a cube sitting in a gap is not connected to the plate and escapes the wave. So the press counts 1, 3, 9, 27, 79, 237, 711, 2133, 6399, not exact powers of 3.
- **Pile density:** cubes pack DENSER than the balls did. At K 0.86, both piles turned to all-dust (6561) without overflowing (tops at about 690 vs MAX 560). K 0.95 restores the race.
  - At K 0.93, seed 9 runs to 37 s and the hammer wins. The race is sensitive to K.
- Crack: each crushed cube shows a white Y crack between its 3 pieces for 0.15 s, the parent's square outline expanding out, 4 corner ticks, and the soft own-colour glow.
- Sound:
  - Same Für Elise notes (merging and gains as press_split2).
  - The crunch is now `synth_cube_crack`: a woody knock (inharmonic bar modes at 1250 → 630 Hz by size), a glassy 4.3-5.6 kHz tick, a 1 ms click edge and a small body thump. There is no noise tail.
  - The machine sounds, the press-release hiss and the riser are unchanged from press_split2.
- Seed search: seeds 0-23 at K 0.95; seeds 0-11 at K 0.95 were run first. The press wins on every seed.
  - Overflows inside the 22-26 s window leave the hammer 150-230 px under MAX.
  - Closer races (about 90 px under) only end at 29-32 s.
  - Picked **seed 9**, timings in clip time:

    | Event | Clip time |
    |---|---|
    | First hammer split | 0.15 s |
    | First press split | 0.20 s |
    | Both counters at 3 | 0.3 s |
    | LEAD CHANGE (the press's last wave, 2133 → 6399) | 22.87 s |
    | PRESS OVERFLOWS (6,399 vs 4,161; hammer pile top 726, 166 px under MAX) | 24.43 s |
    | Plate snaps / eruption | 24.83 s |
    | Dissolve starts | 25.65 s |
    | Clip ends (1575 frames) | 26.25 s |

  - Alternates: seed 21 (overflow at clip 25.6 s, hammer 150 px under) and seed 14 (three lead swaps, overflow at clip 26.0 s).
- Checks (encoded Full HD):
  - Video: h264 yuv420p 1080x1920 60 fps, 26.25 s.
  - Loudness: -13.99 LUFS, peak -6.7 dBFS.
  - Tail: the bed fades to 0 over the last 0.6 s, the same as press_split2's dissolve. The last 0.1 s peaks at -16 dB and is 0 at the seam.
  - Seam mean delta 1.38, the same as press_split2 (1.39). A normal step scores about 1.05 there, because the hammer is falling.
  - flash_check: 1 flash, PASS (mean luminance 0.044).
  - Notes: 67, 9 distinct, top pitch 18 %. Per 5 s: 8, 15, 9, 17, 18.
  - Frames read at 0, 0.3, 1, 3, 13, 22.9, 24.45, 24.9 and 25.6 s, plus frames 9, 12, 1573 and 1574 (the last frame is the pre-roll state that matches frame 0). The 1:1 crops were the crack frame and the overflow pile.
- Known nits:
  - The late dust piles are foamy, with columns and voids, as in the parent.
  - A rotated drawn cube can overlap a neighbour by a few px while it tumbles, because collision is axis-aligned.
- Cost: sim about 1.5 min; Full HD render about 12 min (encoder `-threads 2`, BLAS threads 1).
- Args are the same as press_split2. `--seed` defaults to 9.
- Delivered <VIDEOS_DIR>\batch41\press_split5.mp4 (Full HD). Owner review: pending.

Owner review (2026-10-18): dropped.

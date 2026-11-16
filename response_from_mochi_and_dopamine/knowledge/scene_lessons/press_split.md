# press_split — Hydraulic PRESS vs Drop HAMMER: every crushed ball splits into 3

- Brief: coordinator task 2026-10-13 (batch31). This is a FORMULA TEST (research/reference_satisfying2dsims.md): one rule, one counter per side, neon outlines on pure black, a tension-first opening, an exponential count, about 45 s. Where docs/BRIEF_batch25.md disagrees (orchestra, 20-30 s, payoff-first frame 0), the formula wins.
- Caption (baked; `--cap ''` gives the base without it):
  - "Every ball ~CRUSHED~ splits / into 3 ~SMALLER~ ones": 66 px, CRUSHED and SMALLER in gold.
  - Stake line: "Press or Hammer: which OVERFLOWS first?" (44 px).
- Rule: a crushed ball pops into 3 balls at 0.66× its radius. Generations: R0 = 100 px, then 66, 44, 29, 19, 12.5, 8.3, 5.5, 3.6.
  - Each piece puffs up a little: area ×1.31 per split. This deliberately departs from the brief's r/√3. With area conserved, the pile can never rise, so a chamber could never overflow.
  - A ball under 4.5 px is DUST: it gets pushed but never splits.
  - Children are immune to the stroke that made them.
- **Mochi = HYDRAULIC PRESS** (left), a full-width plate.
  - On contact, a pressure wave runs through the contact graph from the plate, one hop per frame. Every ball connected to the plate is crushed ONCE per stroke, and a ball in the air escapes.
  - So the count goes exactly 1, 3, 9, 27, 81, 243, 729, 2187, 6561.
  - The stroke lifts 330 px above its last stop. Down 105 px/s, squeeze 70 px/s until it stalls (1.2 px residual overlap), hold 0.3 s, up 450 px/s.
  - The down-to-down period runs from about 5.8 s and shrinks 0.15 s per stroke, so the press speeds up.
- **Bolt = DROP HAMMER** (right), a narrow head (116 px) on a carriage that ping-pongs across 8 stops.
  - Free fall at 7000 px/s² from the latch at y 470, lift at 1700 px/s.
  - The blow has a crush budget of 0.27 × (drop + 60) × 100 px² of ball area, spent nearest-first along the contact graph (≤ 10 hops; dust passes the blow on at 0.06 of a hop).
  - A stray dust grain does not stop the head; a bed of 14 dust balls does.
  - It wins early with many quick local gains, then slows as its own dust cushions the blows and the drop height shrinks.
- Physics:
  - numpy position-based dynamics: 2 substeps × 7 averaged-Jacobi iterations, ω 1.5, G 2400.
  - Shock propagation: the lower ball of a pair weighs 1/0.3.
  - Per-generation KD-trees (scipy) for the broad phase.
  - Caps: a contact push may create at most 240 px/s; speed inside a pile (2+ contacts) is capped at 260 px/s; granular damping 0.93 per substep; wall restitution 0.35.
  - Without these caps a dense pile boils or erupts. The sqrt(count) normalisation boiled the mixed-size hammer pile, and the plain average fixed it.
- Overflow: 3 % of a chamber's ball area sits above the MAX line (y 560) for 8 frames. The machine jams, shakes and sparks, and cracks spread across the plate. 0.55 s later the plate snaps in two, the halves fly, and the compressed pile ERUPTS out of the top (the ceiling and machine collider are removed; there is an upward impulse that decays with depth). Winner banner.
  - First try, the outer wall broke and the pile poured out sideways. The 36 px left margin swallowed it all, so it was dropped.
- Seed 8 (searched over 0-32; every seed gives the same story shape, and seed 8 has the smallest margin):
  - Counts M/B (press/hammer):

    | Time | Press | Hammer |
    |---|---|---|
    | 2 s | 3 | 5 |
    | 10 s | 9 | 139 |
    | 20 s | 81 | 2189 |
    | 30 s | 729 | 3673 |
    | 36 s | 2187 | 4139 |
    | 40 s | 6561 | 4607 |

  - The hammer leads from about 2 s to 38.3 s. LEAD CHANGE at 38.32 s, mid-way through the press's last wave (2187 -> 6561).
  - PRESS OVERFLOWS at 39.68 s, with the hammer pile 34 px under MAX (4,567 balls). Eruption at 40.23 s.
  - Clip 42.75 s (2565 frames).
- Hook:
  - Frame 0: one ball in each chamber, the press plate already mid-stroke and the hammer mid-fall, caption fully visible.
  - Hammer's first crush at 0.23 s (1 -> 3); press's at 0.55 s.
  - Readable at 200 px.
- Look:
  - Pure black; chamber outlines are neon (coral for the press, mint for the hammer).
  - Machines: neon outline + dark fill.
  - Balls: coloured by generation (gold, orange, red, magenta, violet, blue, cyan, green, lime). This shows the press's uniform layers against the hammer's mixed pile.
  - Every crush: an expanding ring, plus 6 white ticks for big balls.
  - Labels HYDRAULIC PRESS / DROP HAMMER at y 1398; counters "Balls: N" at 62 px, y 1482 (0.77 h), gold while leading.
  - Mochi and Bolt are r 24 between the labels and react to the race: Bolt cheers early and laughs at 14 s, Mochi is worried, the lead change flips them, and at the end the winner cheers and the loser is annoyed.
  - Banners at y 930: LEAD CHANGE!, OVERFLOW!, PRESS WINS!.
- Layout: chambers x 36-492 and 548-1004, y 330-1330 (0.693 h). The right-edge strip is just the hammer chamber's wall.
- Sound: all built in `build_audio` as a bed (the sidecar holds the note events with note_gain 0).
  - Melody: one marimba note per crush, walking **Für Elise** (Beethoven, WoO 59, 1810; Beethoven d. 1827 -> PD; `audio.MELODIES["fur_elise"]`, top note E5).
    - Crushes merge into at most 1 note / 75 ms; 6 or more crushes in a window adds the octave below.
    - Hammer blows play 1-2 notes each, and press waves play runs of 9-15 notes.
    - 85 notes in all; notes per 5 s: 7, 6, 10, 9, 8, 12, 14, 19 (climbing).
  - Splits: a squelch per split (`synth_squash`), at most every 30 ms per chamber, ducked by local density.
  - Press: low thunk + soft clank on contact, `synth_hiss` on release.
  - Hammer: soft clank + small thunk per blow, quiet latch tick on release.
  - Jam: clank + thunk + a rolled A-minor cadence.
  - Break: 3 glass breaks + boom.
  - Everything ends 0.65 s before the rewind with a 0.35 s fade. `peak_db=-4`.
- Loop: a 1.3 s eased rewind of the stored frames back to frame 0. The last frame is frame 0's state.
- Checks (encoded Full HD, seed 8):
  - Video: h264 yuv420p 1080x1920 60 fps, 42.75 s.
  - Loudness: -14.01 LUFS, peak -4.5 dBFS.
  - Tail: T-1.3 s -39 dB (reverb tail) falling to -53 dB at T-1.0; last 0.5 s -73 dB.
  - Seam mean delta 0.317 (good band).
  - flash_check: 3 flashes, worst 1 s = 2 at 40.17 s (the eruption), so PASS with little margin.
  - Mean luminance 0.045.
- Encoded frames read at 0, 1, 2, 3, 10, 25, 38.4, 39.7, 40.5 and 41.5 s, plus the 200 px thumbnail.
- Known nits:
  - A few dust balls stack in a one-ball column against the hammer chamber's walls above the pile. It is a frictionless-wall artefact, and small at 1:1.
  - The late piles look foamy, with voids, rather than crystal-packed.
  - The file is 126 MB at crf 18 (thousands of particles).
- Cost: sim about 2-5 min (depending on load), Full HD render about 12 min.
- Args:
  - `--seed` (8), `--label`, `--cap`.
  - `--still --frame a,b,c`, `--report`, `--search A B`.
  - `--reuse` re-mixes the audio over an existing `_silent.mp4` without re-rendering.
- Delivered <VIDEOS_DIR>\batch31\press_split.mp4 (Full HD). Owner review: pending.
- Owner review (2026-10-13): good; make it faster with better, research-based colours -> press_split2.

# neon_trails — cyberpunk light-trail duel (batch25, 2026-10-10)

Owner request: "popular things from pop culture without copyright issues: anime, cyberpunk, gaming". This is the generic light-trail duel trope: "neon bikes" and "light trails". No IP names, brand designs or logos.

## Rule
- Seven neon bikes ride a 20x24 grid arena in steep perspective (synthwave sun, rain-wet skyline, glitch accents).
- Every bike leaves a solid light wall. Hitting any wall or the rim = OUT.
- A crashed bike's wall de-rezzes over 3 steps and leaves a flat floor burn mark, which is not a wall.
- Last bike riding wins.

## Engagement: algorithm vs algorithm (real grid AI, deterministic, moves resolved in turn)
- **MOCHI, "MOST OPEN SPACE":** flood-fills the arena from each possible move and takes the one with the most reachable cells. Ties go to the most open 7x7 patch.
- **BOLT, "CUT-OFF":**
  - He seals her into a box when a move wins him the space battle (her side ≤ 100 cells and < 0.7 of his).
  - Otherwise he keeps contact and runs for the cell 5 steps ahead of her (shortest path).
  - Once they are sealed apart, he fills by wall-hugging.
- **5 neutral bikes:** they ride straight and turn when bored. Their skill = reflexes at a wall, so they crash out one by one: neon shatter, pillar, floor ring, local glitch slices.
- **HUD:**
  - The floor tint and the bar show who owns the space (Voronoi: the cells each one reaches first).
  - When they are sealed apart, the HUD switches to the true CELLS LEFT.
  - "RIDERS: n" counts the bikes still riding.
- **Story, seed 149:**
  - Neutrals out at 2.52, 2.91, 5.12, 6.31 and 9.83 s, then the "1 vs 1!" banner.
  - "BOXED IN?!" at 12.02 s: her 27-cell box glows red, with a spotlight and a ring on the gap.
  - **"1-CELL SQUEEZE!" at 13.07 s:** Mochi slips through the last cell next to Bolt's nose (Bolt 1 cell away). This lands on the big diminished chord.
  - The SPACE lead swings late (2 lead changes after the squeeze).
  - They are sealed apart at step 94.
  - **Bolt crashes at 16.45 s, on the final D-minor chord.**
  - "MOCHI WINS! with 14 CELLS to spare": Mochi cheers, Bolt gives the annoyed stare, and a sparkle runs her whole trail.

## Seed search (`--search a n`)
- The game is never edited. We pick a seed, plus the AI parameters it draws (look 5, box 100, straight 2, neutral skill 0.18-0.80), whose squeeze and finale fit the music. Then the clock is fitted:
  - Adagio quarter = 0.85 s.
  - Step speed ramps 4.56 → 6.80 cells/s through the Adagio.
  - The drop at 102 bpm, with bikes stepping on the 16ths (4 per beat).
  - The sequence enters at beat 32 (whole sequence units cut).
  - Fermata on the big chord = 1.62 s.
- Hit rate is about 1 in 200 seeds on 20x24. The score rewards a close finish, late lead changes, a squeeze near the camera, a fast launch and T ≥ 19.8 s.
- Seed 149 is the closest finish found in ~1.5k seeds. Bolt-win alternatives exist (1110: 37 cells to spare; 428: 63) but they are less close.

## Hook / loop
- **Frame 0 = the payoff:** the final coral and mint labyrinth plus the rainbow burn marks of the 5 neutrals, with the winner's bike.
- 0.04-0.72 s: everything de-rezzes back to the start grid (trails retract, glitch slices, neutrals materialise). "GO!" and the launch come at 0.85 s, on the mordent's landing D.
- The clip ends on the same frozen labyrinth.
- Seam: pre-encode 1211→0 = 0.0523, equal to the hold's own frame delta (0.0523, rain motion only), so the loop is exact. Rain and window flicker are periodic over T.
- The beat-0 grid pulse starts at 0.04 s, so frame 0 is not brighter than the last frame.

## Music
- J.S. Bach, Toccata and Fugue in D minor BWV 565. Bach d. 1750: public domain.
- **Notes:** copied from the Mutopia Project MIDI, Mutopia-2011/09/11-1780 (Bach-Gesellschaft Ausgabe 1867, "Public Domain"). They are embedded as SEC_A (bars 1-3) and SEC_C (the bar-7 pickup to the bar-12 downbeat), and match chladni_plate2's verified copy.
- **Our synthwave arrangement**, built with `lib/orchestra.py` synth patches (MuseScore_General, MIT):
  - Saw lead = the right hand an octave down.
  - Square lead = the left hand.
  - Synth bass + bass2 = the pedal, plus a D pedal pulse in 8ths under the drop.
  - Warm pad, trance-gated in 8ths and side-chained, plus synth strings on the held chords and a D-minor drone.
  - Synth voice swell on the big chord.
  - Electronic kick, clap and hats from the drop; a heartbeat kick in the Adagio; a snare-roll build through the fermata.
  - Booms at 0.00 s, the D pedal, the squeeze and D minor. Cymbal swells into the drop, the squeeze and D minor.
  - **Every crash = snare + low tom + splash + taiko.**
- **Sync, measured as onset-flux peaks within 0-33 ms of each anchor:**

  | anchor | time (s) |
  |---|---|
  | frame 0 (mordent) | 0.00 |
  | launch | 0.85 |
  | crashes | 2.52 / 2.91 / 5.12 / 6.31 / 9.83 |
  | drop | 8.95 |
  | squeeze | 13.07 |
  | run | 14.69 |
  | final crash = D minor | 16.45 |

- Register: lead tops out at Bb4; nothing shrill.

## Checks (<VIDEOS_DIR>\batch25\neon_trails.mp4, Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1212 frames = **20.20 s**.
- LUFS -14.02, peak -4.78 dBFS, last 0.5 s -90.3 dBFS. The silent tail starts ~1.5 s before the end.
- flash_check: 0 flashes (mean luminance 0.025). All effects are local.
- check_clip seam mean |delta| 0.634 post-encode (good band). This is codec noise from the I-frame at frame 0; the pre-encode seam is exact (above).
- Encoded frames were read at 0, 0.25, 0.5, 1, 2, 3, 6.35, 10.1, 12.5, 13.1, 14, 15.5, 16.45, 16.6, 17.2, 18, 19 and 20.18 s.

## Args
- `--seed 149` (default), `--cols 20 --rows 24` (default), `--cap "line1|~line2~"`.
- `--still --frame 0,0.5s,...`, `--silent`, `--audio-only` (re-mux onto the existing `_silent.mp4`), `--report`.

## Doubts
- **Mochi wins.** BRIEF.md prefers Bolt wins for balance; seed 149 was by far the closest finish.
- The squeeze happens in the far third of the arena (gap row 16 of 24), so it is smaller on screen. The red box, spotlight and ring compensate.
- At 0.5-1.0 s the arena is briefly near-empty (start grid). It is the de-rez → launch beat, with "GO!" on screen.
- The final crash sits at the arena's near-right corner, partly under the Shorts UI button column.
- The music was checked by measurement only, not by ear.

## Owner review
- pending
- Owner review (2026-10-11): remove the two bikes starting from the middle (too many); shrink the board if empty; music -> 80s Miami style -> neon_trails2.

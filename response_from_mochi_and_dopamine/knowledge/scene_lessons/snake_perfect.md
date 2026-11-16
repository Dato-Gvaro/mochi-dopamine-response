# snake_perfect
- New scene (batch39): the "perfect game". A snake eats until its body fills EVERY cell of a 16x16 board. Built to the RESEARCH RULES (research/simple_viral_formula.md). This is the **CHARACTER side** of the A/B test: the snake's head is Mochi.
- Caption (baked, `--cap`; `--cap ''` = base): `Every bite makes her ^LONGER^|~Until EVERY cell is full~`. The only other text is the readout `CELLS LEFT n` at y 1322 (0.69 h). It turns gold at 10 left and becomes `100% FULL` 0.35 s after the last bite.

## World (logical px)
- The board is 16x16 cells of 59 px at x 46-990 (0.917 w), y 300-1244 (0.65 h). It sits on pure black with a faint lattice and a soft frame.
- **Body:** a round tube 0.70 cell wide, with a group glow and a top-left sheen line.
- **Colour:** a rainbow from Mochi's coral at the head to violet at the tail, re-spread over the length every frame.
- **Luminance is UNIMODAL** along the body: coral rises to yellow, then the colour only darkens, capped at Y 0.55 (`--ycap`). This is a flash fix (see Checks).
- **Food:** a red apple with a leaf and a soft red glow. A soft gold ring appears on each bite.
- When 10 or fewer cells are left, the empty cells get pulsing gold outlines.
- **Mochi (the head):** r 33.
  - She looks along her heading and opens her mouth (`chomp`) as the food gets close.
  - On each bite she squashes and grins.
  - With 6 or fewer cells left she switches to `worried` with sweat.

## Solver (honest, guaranteed to finish)
- **Cycle:** a fixed Hamiltonian cycle. It zig-zags the rows over columns 1-15 and returns up column 0.
- **Shortcut rule** (Tapsell-style): she may move to any free neighbour that is strictly ahead of her head and strictly before her tail in cycle order, without overshooting the food.
  - Her body therefore stays in cycle order, and the cells ahead of her stay free, so she can never trap herself.
  - Shortcuts are allowed only while she covers ≤ 50% of the board. After that she follows the cycle exactly (the zig-zag pattern forms). 50% gave the fewest steps; 70% and 100% leave gaps that cost extra laps.
- **Food:** a uniformly random free cell (seeded).
- **Start:** the real game is simulated from length 4. The clip starts at length 102, so 154 bites are left. The sim asserts the board ends full.
- **Seed search** (`--search N`): the first bite has to be 4-14 steps away, and the last 3 cells have to be 3/2/1 or 2/2/1 steps apart. Among those, the search minimises steps. 1,200 seeds were searched; s825 uses the fewest: 4963 clip steps, first bite 7 steps away, last 3 cells 3/2/1.
- Tapsell's cycle allows only forward shortcuts, so trips are long (mean 32 steps per bite). That is why the snake is fast in mid-game.

## Clock (clip time = a warp of game steps)
- Each bite c gets an interval ∝ (local mean of distance-ratio)^0.75 / (1 + 1.5·u), where u runs 0 → 1 over the clip. The intervals are scaled so bite 150 (3 left) lands at 28.0 s, with a minimum of 0.065 s.
- A ritardando (×1.2-2.2) covers bites 147-150. The last 3 cells take a fixed 0.62 / 0.78 / 0.95 s.
- **Step position:** a PCHIP curve through the bite knots, so it is monotone and smooth with no jumps.
- **Last 3 cells:** she threads them one cell at a time: a 45% hold, then a smoothstep. Each step gets a soft tick.
- Bites per 5 s: 17 / 22 / 24 / 31 / 34, then 25 in the 25-30 s window, which includes the deliberate slow-down. Cells per frame by 5 s: 2.9 / 3.5 / 3.9 / 3.2 / 2.4 / 0.6 (max 5.8).
- First bite 0.40 s. Shortcuts end at bite 26 (~6 s). 3 LEFT at 28.0 s, 2 LEFT at 28.62 s, 1 LEFT at 29.40 s, full board at **30.35 s**.

## Finale (last bite + 0 → 4.0 s)
- A ripple runs from tail to head over 1.3 s: a whitened, 1.3x-wide band.
- Then the BLOOM: the whole body lifts toward white (0.22), a soft gold radial glow peaks at alpha 0.20, and 54 star twinkles appear on random cells.
- Mochi grows 1.32x, grins and bobs.
- The zoom goes 1.0 → 1.07 → 1.0 by +3.3 s.
- At +3.4 s a 0.6 s dissolve runs into the real pre-roll game, so the loop is seamless.

## Sound
- **Melody:** Scott Joplin, *The Entertainer* (1902, PD). It is not in `kit.KID_CODED_MELODIES`.
  - **Source:** Mutopia Project, `mutopiaproject.org/ftp/JoplinS/entertainer/entertainer.mid`, licence Public Domain, cached in `<SOUNDFONTS_DIR>\scores\joplin_entertainer\`.
  - The lead is the RH top voice, onsets 16-169 (the A strain twice), with octave doublings collapsed to the lower note: D4-E5. That is exactly 154 notes for 154 bites.
  - `--verify`: **LEAD matches the source MIDI: True**.
  - `audio.MELODIES['entertainer']` was not used: its second phrase does not match the score.
- **Note per bite.** The last 3 cells are the cadence B4-D5-C5, and the final bite is the C.
- **Instruments** (soundfont, MuseScore_General):
  - Piano lead. A harp doubles it an octave down in the second A strain.
  - Joplin's LH oom-pah (272 notes from the same MIDI) plays on soft piano, warped onto the bite clock (score beat → time is linear between bites), with pizz on the bass notes.
  - A soft string pad holds the LH harmony per beat.
- **Final bite:** a rich C-major chord (strings + rolled piano, top C5), contrabass C2, timpani C and a soft boom.
- **Ripple and bloom:** a rising C-major harp run synced to the ripple (tail → head), then a choir swell + a celesta C5 at the bloom.
- **SFX (synth):**
  - A soft crisp **chomp** per bite, +12 ms off the notes: a 560→230 Hz falling pok, a 0.9-2.8 kHz click and a tiny crunch 14 ms later.
  - A very soft wooden **tick** only on steps ≥ 0.1 s apart (4 in the clip: the opening and the final threading).
  - Every SFX onset is ≥ 12 ms from every note. There is no hiss or whoosh; energy above 3 kHz is 0.08%.
- -14.00 LUFS, peak -7.77 dBFS. The last 1.0 s is digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx` (0.16) `--search N --from S --verify`. Tuning: `--build` (28.0) `--ratex` (2.5) `--gamma` (0.75) `--ycap` (0.55).

## Checks (encoded Full HD, s825)
- h264 yuv420p 1080x1920, 60 fps, 2061 frames = **34.35 s**.
- **flash_check PASS:** 4 flashes, worst 2 per 1 s (finale), mean lum 0.067.
  - The first render FAILED with 22 flashes. In the cycle phase every cell sees the whole gradient pass once per lap (~1 s), and a plain rainbow is bright-dark-bright-dark.
  - The unimodal luminance alone still failed (3 per 1 s). The Y cap at 0.55 fixed it.
- **Seam:** pre-encode last → 0 mean delta 0.096 against a normal step of 0.094 (frame nf-1 = pre-roll frame -1). Encoded seam 0.485.
- Encoded frames read at 0 / 0.5 / 1 / 2 / 3 / 17 / 29.1 / 29.9 / 31.6 / 33.0 s, plus a Full HD crop at 1 LEFT: the worried face, sweat and apple read at 1:1.
- Render ~5 min (Full HD).

## Doubts
- **Mid-game speed is 3-4 cells/frame** (up to 5.8). Total steps are fixed by the honest solver (~4,960), so in mid-game Mochi is a zipping head and the rainbow flows. Her face reads at the start, at 10 left and in the finale.
- **Snake speed FALLS late while bites accelerate.** That is geometry: with fewer free cells, the food is nearer. The brief's "speed rises" holds for the event rate, not the head speed.
- The last-5-s bite rate drops by design for the 2.35 s "3/2/1 LEFT" tension.
- Bite rhythm is irregular (note per bite, as in ring_burst). The LH is warped to it, so the accompaniment is rubato. This was not heard by a human yet.
- The yellow is slightly olive because of the flash cap.
- 34 s is inside the research 25-40 s window but above our channel's 15-20 s data rule.

Delivered `<VIDEOS_DIR>\batch39\snake_perfect.mp4`. Owner review: pending.

Owner review (2026-10-17): rejected ("we already had a snake thing that did not go well"); replace with a format from successful physics/maths-satisfying channels.

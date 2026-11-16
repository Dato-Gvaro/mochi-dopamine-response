# press_break — press_split2's sequel: "until one machine BREAKS"

- Brief: coordinator task 2026-10-21 (batch46). The sequel to press_split2 (112K views, 77.6 % stayed), made inside the 14-day sequel window (research/early_breakouts.md).
- **THE ONE CHANGE is the STAKE.** Each machine has a STRAIN meter (0 → 100 %), with a red BREAK cap visible from frame 0. The race ends when a machine BREAKS, not when a chamber overflows. The machine that breaks loses.
  - The MAX line and the overflow are gone (one end state only).
  - Everything else is press_split2: one ball per chamber, both machines already moving at frame 0, every crushed ball splits into 3, Mochi = hydraulic press, Bolt = drop hammer, the palette, the faces, a Für Elise note per crush, and the dissolve loop.
  - The owner rejected cosmetic sequels (×4 = press_split3, cubes = press_split5). This one changes what the video is about, not the look.
- New file; press_split2 stays bit-reproducible. The stage uses press_split4's side-safe layout (stage ×0.815 about x 0.47w; walls x 110–905).
- Caption: "Every ball ~CRUSHED~ splits / into 3 ~SMALLER~ ones / until one machine ~BREAKS~". Line 3 is 56 px, with BREAKS in coral red. I chose it over "How many can each one HANDLE?" because it names the end state, and the word matches the BREAK caps on the meters.

## Load model (honest-ish, from the sim's own crushes)

- Every ball a machine crushes loads that machine by **its size × the stroke's speed factor**: `strain += (r / R0) × w / RATING`. RATING = 126 for BOTH machines.
- **Press:** a steady squeeze, w = 1. But the full-width plate crushes the WHOLE pile every stroke (3× the balls at 0.66× the size), so the load per stroke roughly doubles (×1.98): 1, 2, 3.9, 7.8, 15, 30, 60, 119.
- **Hammer:** an impact spike, w = v_impact / 3500 px/s. That is about 1.0 on the first long drop and less once the pile rises. The narrow head only crushes what one blow's energy reaches (press_split2's budget model). So the hammer climbs fast early and softens as its balls get small and the drop shrinks.
- Strain is fatigue: it never goes down. Hairline cracks appear on the housing, plate/head and cylinder from 75 % strain, growing with the meter, so the hammer's near miss shows too.
- Tuned offline (scratch `pbreak_tune.py`): the two chambers are independent, so one uncapped sim per seed gives the exact strain curves for any (size exponent, V_REF, RATING).
  - Searched size exponent 0–1.5, V_REF 2000–4500, RATING 40–3000, a v² variant, seeds 0–3.
  - Kept: size¹ × v¹, the simplest model that gives one late strain lead change and a close finish. A v² variant moved the early meter more but needs a size^1.25 fudge.
- Press periods are 0.3 s quicker than press_split2 (P_PER0 3.6, P_PER_MIN 2.4), which brings the clip under 25 s.

## Seed 1 (clip time)

- Seed search (0–3) gives the same shape on every seed. Seed 1 is the closest finish with one lead change and the survivor under 97 % at the end.
- First splits at 0.17 s (hammer) and 0.18 s (press). Counters read 3/3 and both meters 0.7 % by 0.3 s.
- Press strokes at 0.17, 2.75, 6.1, 9.3, 12.5, 15.5, 18.2 and 20.7 s.

  | Time | Press balls | Hammer balls | Press strain | Hammer strain |
  |---|---|---|---|---|
  | 3 s | 9 | 15 | 2.4 % | 3.3 % |
  | 8 s | 27 | 253 | 5.5 % | 18 % |
  | 12 s | 81 | 1,405 | 12 % | 47 % |
  | 16 s | 729 | 2,411 | 48 % | 68 % |
  | 20 s | 2,187 | 3,315 | 96 % | 85 % |

- The hammer leads the strain race from the start. **STRAIN LEAD CHANGE at 18.45 s**, mid-way through the press's 7th wave (48 → 96 %).
- The press then sits at 96 % with its BREAK cap pulsing and cracks spreading, while the hammer climbs 78 → 92 %.
- **The PRESS BREAKS at 20.87 s**, on first contact of its 8th stroke: 2,425 balls, strain 101 %. The hammer is at 91.9 % (3,653 balls).
  - The housing cracks in two and tilts apart, the cylinder cracks, and the piston rod snaps (the lower piece flies).
  - The plate snaps in two and both halves fly, with chips, 10 nuts, a golden oil spray and sparks.
  - The pile ERUPTS out of the open top, over the caption.
  - There is a short local glow and a stage shake.
  - Banners: "PRESS BROKE!", then "HAMMER WINS!" at 21.72 s.
  - Faces: Mochi wow, then annoyed; Bolt cheers, then laughs.
- The hammer keeps slamming through the payoff (honest) and ends at 96.4 %, a near miss.
- The dissolve runs from 22.08 s. Clip 22.68 s (1361 frames).
- Crushes per 5 s: 30, 311, 984, 1,425, then 408 in the last 2.7 s (the payoff).

## Look

- press_split2's look, plus:
  - **Strain meters** at y 420 over each chamber. A dark bar fills green → gold → orange → red. A white spike glow shows when the strain jumps (every hammer blow). The text reads "STRAIN 0.8%", with one decimal under 10 % so early blows visibly tick it. A red **BREAK** cap marks the 100 % end; it pulses from 80 %, and the bar reads "BROKEN!" after the break. The bar jitters slightly from 85 %.
  - Hairline cracks from 75 %, and the machine shakes slightly from 85 %.
- The MAX line is removed. The violet chambers, palette, bursts, faces and counters are press_split2's. The counters stay white, because the strain race is the stake.
- The press cylinder is a separate block, so the rod can snap below it.

## Sound

- One note per crush, merged to at most one per 60 ms, walking **Für Elise**: Beethoven WoO 59, 1810, PD.
  - Notes copied from the **Mutopia MIDI** (piece 931, `fur_Elise_WoO59.mid`), right hand, ticks 0–7296: bars 1–8 with the first ending, then the second ending and the C-major episode (54 notes). No lib/audio.py MELODIES.
  - The melody stops at the break.
- Crunch per split (press_split2's). The press thunk + clank and the hammer clank + thunk + latch are press_split2's. **No release hiss** (press_split2 had one; the brief bans hiss).
- **Tension:** a soft metallic gauge ping (bell partials 1 / 2.76 / 5.4, no noise) each time a machine passes another 10 %.
  - The pings climb E3 A3 C4 E4 A4 C5 E5 G#5 A5, panned to that machine.
  - The press's 7th wave fires five pings in a fast rising run.
- **Break:** thunk + slam (with crunch) + clank + two light glass cracks (the gauge glass) + nuts landing.
  - Then the cadence: a rolled A-minor chord, A1–E5, with a soft sustained pad.
  - A tonal riser (no noise) leads into the breaking stroke.
- **Mastering, `peak_db=None`:** master() limits peaks when it drives the mix up to -14 LUFS, so loud break transients cost loudness.
  - The break is light transients (thunk 0.5, slam 0.35) plus a full sustained chord (1.0, pad 1.0). It lands +4.4 dB over the body median (momentary 400 ms) and is the loudest moment in the clip.
  - A heavier version (thunk 1.6, slam 0.9) measured only +1.3 dB.
- Post-master fade: the last 0.5 s is digital silence (faded over 0.6 s before that), re-muxed with the video copied and no `-shortest`.

## Checks (encoded Full HD, <VIDEOS_DIR>\batch46\press_break.mp4)

- Video: h264 yuv420p 1080x1920, 60 fps, 22.68 s (1361 frames).
- Loudness: -14.00 LUFS, peak -5.9 dBFS. The last 0.5 s is silent (-240 dB).
- flash_check: 0 flashes = PASS (mean luminance 0.029).
- Loop seam:
  - Pre-encode, the seam is 0.622, the same as a normal step at the start (0.634). The last frame is the sim frame just before frame 0.
  - Encoded, the seam is 0.911 against normal steps of 0.62–0.66. The extra is keyframe coding.
- Notes: 53, 12 distinct; top note E5 at 17 %. check_clip events per 5 s: 9, 18, 14, 12.
- Side safe zone, measured on encoded frames 0, 19.5 and 20.83 s:
  - Caption 0.109–0.833 w.
  - Meters 0.106–0.834 w.
  - Stage 0.098–0.841 w (wall glow; the walls are inside).
  - Counters, labels and faces 0.128–0.812 w.
  - Only decoration (shards, nuts, oil, sparks, erupting balls) flies wider.
- Frames read from the encoded file at 0, 0.3, 1, 3, 12, 18.45 (lead change), 19.5, 20.83, 20.87 (the break, plus a 1:1 crop), 20.93, 21.03 (1:1 crop), 21.25, 21.58, 22.17 and 22.67 s.

## Nits / doubts

- Strain is a designed model, not measured mechanics.
  - Same rating for both machines; load per ball = size × speed factor. The constants (V_REF 3500, RATING 126) were chosen so the race has one late lead change.
  - It is honest in that the outcome follows from the sim's own crushes. But the press breaking is guaranteed by its ×2-per-stroke load: this is "the press can't HANDLE the whole pile", not a surprise.
- The early meters are small: 0.7–3 % for the first 3 s. That is inherent to ×3 growth, and the decimal readout makes the ticks visible.
- Notes per 5 s are flat (14, 14, 14) rather than climbing, then the cadence. The crush rate does climb.
- Frame 0 is press_split2's (one ball per chamber + meters), not a full multi-hue frame. The full frame comes at the climax.

## Args and cost

- Args: `--seed` (1), `--rating` (126), `--vref` (3500), `--pr` (1), `--per0` (3.6), `--permin` (2.4), `--tlimit`, `--label`, `--cap`, `--still --frame a,b`, `--report`, `--search A B`.
  - `--cache` pickles/reuses the sim in output/.
  - `--reuse` re-mixes audio over an existing `<name>_silent.mp4`. deliver() deletes it, so first rebuild it with `ffmpeg -i <name>.mp4 -an -c:v copy <name>_silent.mp4`.
- Cost: sim about 3 min; Full HD render about 9 min at 2 encoder threads.
- Delivered <VIDEOS_DIR>\batch46\press_break.mp4 (Full HD). Owner review: pending.
- **4K ship render** (2026-10-21, coordinator, same sim cache, no changes): `output/press_break_ship_9x16.mp4`, h264 yuv420p 2160x3840 60 fps, 22.68 s (1361 frames), 82 MB. -14.00 LUFS, peak -5.89 dBFS, last 0.5 s silent, seam 0.808, flash_check 0 flashes = PASS. Notes and events match the Full HD cut.

Owner review (2026-10-21): "it looks exactly same, we need a little bit something different but not to go far from researched thing" -> unstaged; rebuild as press_break2 (new look/layout, same x3 + break stake).

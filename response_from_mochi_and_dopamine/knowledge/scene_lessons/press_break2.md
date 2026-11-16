# press_break2 — "How many until the press BREAKS?" One giant hydraulic press

- Brief: coordinator task 2026-10-21 (batch47), from the owner's review of press_break: "it looks exactly same, we need a little bit something different but not to go far from researched thing".
- The skeleton is press_break's: one ball, every crushed ball splits into 3, the press crushes the whole pile every stroke, the end state is the press BREAKS, then a break finale.
- The look and layout are new, modelled on the parent's "How many balls does it take to break a hydraulic press?" (331K). New file; press_break and press_split2 are untouched.
- Caption (2 lines, 66 px): "Every ball ~CRUSHED~ splits into 3" / "How many until the press ~BREAKS~?" (BREAKS in red).

## Look / layout (all key elements measured inside 0.102–0.838 w)

- **ONE industrial press**, centred:
  - Hazard-striped yellow/black columns (x 118–182 and 834–898).
  - A steel crosshead with bolts (y 330–440) and a steel cylinder.
  - A chrome piston rod and a steel platen with a hazard band.
  - A steel bed at y 1300 (0.68 h). The pit is x 190–826.
- **Pressure gauge** on the cylinder, r 112, centre (508, 432):
  - Green/amber/red zones (red from 80 %) and a dark BREAK wedge past 100 %, with a "BREAK" label.
  - The needle swings up with each stroke's load and falls back on release (damped). Every stroke is a new attempt.
  - A red **peak pointer** keeps the record.
  - Digital "%" readout. The needle and platen shake when the load is past 70 %.
- **Rainbow confetti pile:** each child takes its parent's hue −38°, +0 or +38°, so the pile turns multi-hue. Size by generation as before; the first ball is r 100, gold.
- **Bettors:** Mochi (left, x 196) and Bolt (right, x 820) sit under the bed with signs from frame 0: "BREAKS BEFORE 500" (v1: 200) and "BREAKS BEFORE 5,000".
  - When the count passes 500 and the press still holds, a "PASSED 500!" banner pops and Mochi's sign is stamped WRONG.
  - At the break, Bolt's sign is stamped RIGHT, because 2,041 < 5,000: "BOLT WINS!".
  - Faces: Mochi worried at each early stroke, then wow and annoyed; Bolt laughs, worries in the red, then cheers.
- Counter "BALLS: N" (64 px, y 1468) with a gold **×3** badge.
- Pressure cracks on the columns and crosshead appear at record pressures of 62–97 %.
- **Break:**
  - The crosshead splits and tilts apart, and the right column buckles.
  - The gauge glass shatters and the needle pegs at BREAK, with "BROKEN!" on the readout.
  - The rod snaps and the lower piece flies. The platen snaps in two and both halves fly, with chips, 12 nuts, oil spray and sparks.
  - A local glow and a stage shake.
  - The compressed rainbow pile ERUPTS over the gauge and caption.

## Load model (honest-ish)

- A ball's crush resistance is its cross-section, (r/R0)². A stroke's load is the sum over the balls it has crushed so far, and the needle shows load / RATING.
- The platen crushes the WHOLE pile every stroke: 3× the balls, each 0.4356× the area. So the peak load per stroke grows ×1.31: 1, 1.31, 1.71, 2.23, 2.92, 3.81, 4.98.
- RATING 4.48 puts stroke 6 at 85 % (deep in the red; it survives). Stroke 7 crosses 100 % about 90 % of the way through its squeeze, so the press breaks at **2,041 balls** (v1: 2,049; v2: 2,057).
- The count is the sim's, not scripted. RATING was picked for the gauge drama: stroke 6 in the red, stroke 7 breaks.
- The crushes run layer by layer from the platen. The wave takes at least 3 frames per contact hop, and the pump-power law (v3, see the timeline) sets each stroke's duration: stroke 5 1.4 s, stroke 6 3.4 s, stroke 7 5.6 s to the break.

## Timeline (clip time, seed 0), v3 (2026-10-21)

- **History:**
  - v2 fixed the opening (owner: "a strong effect within the first 2 seconds, then you can go slower").
  - v3 fills the middle (coordinator: 3–12 s was two strokes at −31 dB RMS).
- **Limited pump power (honest slowdown):** the harder the pile pushes back, the slower the squeeze.
  - At first contact, the whole crushable pile in the pit weighs S (load units). The stroke takes **S³ / (3 P)** s, with P = 5.5 (dL/dt = P / L², integrated).
  - Its crushes are spread evenly over that time, layer by layer from the platen (contact-graph hops, then height), and no faster than the wave (3 frames per hop) reaches them.
  - So light early strokes are instant hits, and the heavy late strokes are long continuous squeezes. The needle creeps up through each one.
  - Durations: stroke 5 1.4 s, stroke 6 3.4 s, stroke 7 5.6 s to the break.
- **Between strokes:** the gap is `0.10 + 0.05·(L−1)` s (cap 0.6) and the lift `30 + 25·(L−1)` px. The platen moves at 450 px/s down and 900 px/s up.
- The clip starts 2 frames before stroke 2 lands (stroke 1, 1 → 3, is before the clip). The loop dissolves into the frames just before that.
- **On screen:**
  - **0 s:** 3 balls (green, gold, red), the platen coming down, the peak pointer at 22 %, and the signs "BREAKS BEFORE 500" / "5,000".
  - **0.08 s:** first split.
  - **0.5 s:** 9 balls; the needle jumped to 29 %.
  - **1 s:** 27 balls; the gauge at 38 %.
  - **2 s:** 81 balls; the gauge peaked at 50 %.
  - **3 s:** 177 balls, mid-squeeze (needle 39 %).
  - **6 s:** 531 balls (needle 50 %, record 65 %).
  - **9 s:** 967 balls.
  - **12 s:** 1,551 balls (needle 63 % and climbing).
  - **14.5 s:** 2,037 balls, needle at 100 %.
- **Strokes:** 0.03, 0.50, 1.12, 2.12, 4.02, 7.78 s. Gauge peaks 29, 38, 50, 65, 85 %, then BREAK.
- **PASSED 500 at 5.80 s**, mid-squeeze of stroke 6. Mochi's bet is stamped WRONG.
- **The PRESS BREAKS at 14.52 s**, at 2,041 balls, during stroke 7's squeeze. "PRESS BROKE!", then "BOLT WINS!" with Bolt's RIGHT stamp.
- Clip **16.33 s** (980 frames).
- **Crushes per second** (0–14 s): 12, 27, 47, 34, 70, 73, 72, 34, 111, 98, 97, 97, 98, 97, then 52 in the last half second.
  - The two dips (34) are the short gaps between strokes.
  - The count climbs every second: 3, 27, 81, 177, 243, 385, 531, 675, 743, 967, 1,161, 1,357, 1,551, 1,745, 1,941, 2,041.

## Sound (v3)

- One note per sampled crush, at most one per 0.10 s (the squeezes crush ~100/s), walking **Für Elise**. The notes are copied from the Mutopia MIDI (piece 931, right hand, 54 notes); no lib MELODIES.
  - A stroke too short to space notes still plays a quick run (up to 5 notes, 65 ms apart).
  - **The melody is rotated so the last note before the break is FUR_ELISE[34], the A that closes bars 1–8 (E C B A).** The A-minor cadence then lands on the break.
  - 131 notes; 9–10 per second during the squeezes.
- Crunch per split (rate-capped), and a press thunk + clank at each contact.
- **Pump ticks:** a soft wood-block tick (620 / 1530 Hz damped sines, no noise) every 0.15 s from frame 0 to the break. The level follows the needle.
- **Gauge pad:** a soft open fifth (A2 E3 A3 E4, light vibrato, no third, so it sits under both the A-minor and the E-major bars). Its level is 0.3 + 0.7 × the needle (smoothed), and it hands over to the cadence at the break.
- **Gauge pings** (bell, no noise) each time the RECORD passes another 10 %, and a tonal riser into the breaking stroke.
- **Break:** thunk 0.5, slam 0.35, clank, two light glass cracks, nuts landing. Then the rolled A-minor cadence A1–E5 at 2.5, plus a pad at 2.5.
  - The busier v3 body needed the bigger sustained cadence: master() limits peaks, so the lift has to come from sustained mid-range.
- Mastering: `peak_db=None`. Post-master fade so the last 0.5 s is digital silence.

## Checks (encoded Full HD, <VIDEOS_DIR>\batch47\press_break2.mp4, v3)

- Video: h264 yuv420p 1080x1920, 60 fps, 16.33 s.
- Loudness: −14.01 LUFS, peak −8.3 dBFS. The last 0.5 s is silent (−240 dB).
- **RMS per second:** −16.6, −16.9, −16.4, −17.1, −16.0, −15.9, −16.2, −16.5, −16.5, −16.0, −16.1, −15.8, −16.1, −16.0, −14.5, −19.8 (the fade). No second below −17.1 dB before the break.
- **Finale:** momentary −11.2 LUFS, the loudest moment. That is +2.7 dB over the body median (−13.9); the body max is −12.1.
- flash_check: 0 flashes = PASS (mean luminance 0.057).
- Loop seam: 0.78 against normal steps of 1.24–1.73 at the start. The last frame is the sim frame just before frame 0.
- Notes: 131, 12 distinct; top note E5 at 17.6 %. check_clip events per 5 s: 44, 51, 36 (the last window ends at the break, 4.5 s).
- Side safe zone, on encoded frames 0, 8 and 14.52 s: caption 0.107–0.836 w, press and gauge 0.103–0.837 w, HUD 0.102–0.838 w.
- Frames read from the encoded file at 0, 0.5, 1, 2, 5, 8, 12, 14.52 (the break, 1:1 crop), 14.75, 15.83 and 16.32 s.

## Nits / doubts

- v3: crushing is continuous from 2 s to the break, except two short gaps between strokes (~0.5–0.8 s each, 34 crushes/s). The pump-power law is a designed model: honest in direction (heavier pile → slower squeeze), with the exponent and P chosen.
- The finale lift (+2.7 dB) is a little under the ~3 dB target. The dense body (continuous crushes + pad) leaves less room under the master limiter.
- The result is predictable once the needle sits at 85 % after stroke 6: Bolt's 5,000 was never in danger. The tension is "when", not "who".
- RATING is a designed constant (honest model, chosen threshold).
- Frame 0 is one big gold ball plus the press and gauge, not a full multi-hue frame. The full frame comes at the climax.

## Args and cost

- Args: `--seed` (0), `--rating` (4.48), `--pow` (5.5), `--gapa` (0.10), `--gapb` (0.05), `--gapmax` (0.6), `--tlimit`, `--label`, `--cap`, `--still --frame a,b`, `--report`.
  - `--cache` pickles/reuses the sim in output/.
  - `--reuse` re-mixes over `<name>_silent.mp4`. Rebuild it first with `ffmpeg -i <name>.mp4 -an -c:v copy <name>_silent.mp4`.
- Cost: sim about 2 min; Full HD render about 7 min at 2 encoder threads.
- Delivered <VIDEOS_DIR>\batch47\press_break2.mp4 (Full HD; v3, the continuous squeezes, overwrote v1/v2). Owner review: pending.
- **4K ship render** (2026-10-21, coordinator, v7 sim cache, no changes): `output/press_break2_ship_9x16.mp4`, h264 yuv420p 2160x3840 60 fps, 16.33 s (980 frames), 47 MB. −14.01 LUFS, peak −8.33 dBFS, last 0.5 s silent, seam 0.580, flash_check 0 flashes = PASS. Notes and events match the Full HD v3.

Owner review (2026-10-22): press_break2 superseded: "we need some new tool… trident vs spike?" -> press_tools.

Owner question (2026-10-22): "you think this is good?" -> my verdict: no, skip it (press_tools covers the sequel; press_break2 has no real tension).

# press_squeeze — two presses squeeze one box TOGETHER from LEFT and RIGHT "until it BURSTS"

- Brief: coordinator tasks 2026-10-22 (batch47).
  - The owner's idea: "pressing from two sides? top and bottom fixed walls and press from LEFT and RIGHT, the characters would be at the press gauges".
  - The owner's review of v1 (presses took turns): "maybe it will be better if they squeeze TOGETHER, not one by one".
- press_split2's look (violet neon box on black, counter, faces, Für Elise note per crush, banners, dissolve loop) in a side-safe layout.
- Caption: "Every ball ~CRUSHED~ splits into 3" / "Squeeze until it ~BURSTS~" (66 px, BURSTS in red).

## v2 mechanics (the shared squeeze)

- **Both plates drive in at once** (300 px/s). When both meet the pile (or 0.3 s after the first does), ONE stroke starts for both.
  - Every crushable ball goes to the plate it is fewer contact layers from.
  - The crushes run layer by layer inward from both plates, so **two crush fronts meet in the middle**.
  - Each ball is crushed once per stroke and splits into 3 (0.66× radius, area ×1.31).
- **Limited pump power (honest slowdown):** the stroke on a pile of load S = Σ (r/R0)² takes **S² / 4** s, with its crushes spread evenly over it. So the crush rate climbs stroke after stroke.
- Each stroke drives each plate at most 30 px past where it met the pile; then both retract 55 px and pump in again (the visible pump).
- **Gauges:** each press's gauge reads the pile density in the 170 px band in front of its own plate, above the loose pile's own density (0.35). It is like a real gauge reading above ambient: needle = (local − 0.35) / (1.0 − 0.35), with a peak pointer.
  - Both climb together with small differences (whose side is under more pressure). The needles shake past 60 %.
  - **The first gauge to hit BURST bursts the box.** That is the light stake: "BOLT BURST IT!".
- **The squeeze reads without big plate travel:** the plates pump in and out each stroke, and the **top wall bows up** (up to 16 px) with the record pressure. **Cracks** spread on the top wall from 70 / 78 / 86 / 93 %.
- **Colour:** balls take an **ordered rainbow by where they were born between the plates**: crimson at Mochi's plate → orange → gold → green → teal → blue → violet at Bolt's. Smaller generations are slightly lighter. Burst rings use the same hue.
  - A first v2 pass mapped the rainbow across the whole box and came out mostly gold-green, since the pile sits mid-box. Mapping it across the plate gap fixed that.

## Layout (side safe zone, measured on encoded frames 0, 10 and 14.7 s)

- **Caption** y 196 / 282: 0.108–0.831 w.
- **Gauges** "MOCHI'S PRESS" / "BOLT'S PRESS" (r 70, at x 318 and 702, y 486), with the characters beside them (r 38, at x 178 and 842): 0.130–0.812 w.
- **Box** x 250–770, y 640–1250. Piston cylinders at x 112–182 and 838–906, and chrome rods. Box + presses: 0.101–0.842 w.
- **Counter** "Balls: N" at y 1408: 0.320–0.619 w.

## Timeline (clip time, seed 0)

- The clip starts 4 frames before the 3rd stroke lands (same sim). The loop dissolves into the frames before it.
- **0 s:** 9 balls (teal / gold / orange), both plates closing in, gauge peak pointers at 20 %.
- **0.07 s:** first crush.
- **0.5 s:** 19 balls; both plates squeezing, both needles at 31 %.
- **1 s:** 27 balls; the plates pump back out, gauges at 34 % (peak 42 %).
- **2 s:** 57 balls, mid-squeeze, both needles at 58 %.
- **6 s:** 311 balls, mid-squeeze. Needles at 69 / 63 % (peaks 72 / 71 %). The first top-wall crack is showing.
- **10 s:** 843 balls, the long squeeze. Needles at 62 / 65 % (peaks 97 / 96 %), the wall bowed, cracks spreading.
- **Strokes:** 0.07, 1.28, 2.92, 5.50, 9.52 s (the last runs to the burst).
- **The box BURSTS at 14.70 s**, when Bolt's gauge hits 100 %, at 1,949 balls.
  - The top wall splits and tilts open, with a glow, a shake, shards and sparks, and the rainbow pile erupts over the gauges and caption.
  - Banners "IT BURST!", then "BOLT BURST IT!". Bolt cheers and laughs; Mochi shows wow, then annoyed.
- Clip **16.62 s** (997 frames).
- **Crushes per second:** 9, 15, 14, 38, 39, 34, 67, 67, 67, 65, 118, 117, 118, 118, then 84 (to the burst).

## Sound

- One note per crush, merged per 75 ms, walking **Für Elise**.
  - The notes are copied from the Mutopia MIDI (piece 931, right hand, the same 54 notes as press_break); no lib MELODIES.
  - Rotated so the last note before the burst is the A that ends the phrase (E C B A), with the A-minor cadence on the burst. 7–12 notes per second.
- Crunch per split, rate-capped, +12 ms off note onsets.
- A soft thunk + clank at both plates on each stroke's contact.
- **Gentle tonal hydraulic pump pulses** (soft low sines with a slight upward glide, no noise): Mochi A2 + Bolt E3 **together**, every 0.24 s for the whole clip, slightly louder as the pressure climbs.
- **Burst:** thunk + slam + light glass crack, then the rolled A-minor chord A1–E5 at 3.0 plus a pad at 3.0.
- Mastering: `peak_db=None`. Post-master fade so the last 0.5 s is digital silence.

## Checks (encoded Full HD, <VIDEOS_DIR>\batch47\press_squeeze.mp4, v2)

- Video: h264 yuv420p 1080x1920, 60 fps, 16.62 s.
- Loudness: −14.01 LUFS, peak −8.8 dBFS. The last 0.5 s is silent (−240 dB).
- **RMS per second:** −17.1, −16.8, −17.3, −16.2, −16.6, −17.0, −16.2, −15.9, −16.1, −16.5, −16.1, −15.8, −15.8, −15.9, −14.8, −16.5. No second below −17.3 dB.
- **Finale:** momentary −11.0 LUFS, the loudest moment, +2.8 dB over the body median.
- flash_check: 0 flashes = PASS (mean luminance 0.023).
- Notes: 152, 12 distinct; top note E5 at 18 %.
- Loop seam: encoded 2.22. Rendering sim frames start−1 → start directly gives 1.99 against a next step of 1.96 (the plates move every frame), so the loop is seamless; the extra is keyframe coding.
- Frames read from the encoded file at 0, 0.5, 1, 2, 6, 10, 14, 14.7, 14.92 (1:1 crop of the burst), 15.5 and 16.6 s.

## Nits / doubts

- **Opening:** the first 2 s are strong but not explosive (9 → 57 balls, two quick strokes). The ×3 per stroke is honest, and the pump law keeps the early strokes short.
- **Gauge plateau:** the gauges' records sit at 96–97 % from about 9 s to the burst at 14.7 s (the last long stroke). That is tension in the red, but the record needle doesn't move. The live needles pump between about 60 and 97 %.
- **Plate travel is small:** the plates pump about 55 px each stroke but stay around x 330–650 (the pile fills the gap). The squeeze reads through the pump, the bowing and cracking wall, the density, and the two crush fronts.
- **Who bursts it** is decided by which local band hits BURST first (Bolt, by about 1 %). It is a light stake, not a race.
- **Finale lift short of target:** +2.8 dB, a little under ~3 dB.

## Args and cost

- Args: `--seed` (0), `--floc` (1.0), `--pow` (4), `--stroke` (30), `--back` (55), `--pause` (0.12), `--tlimit` (30), `--label`, `--cap`, `--still --frame a,b`, `--report`.
  - `--cache` pickles/reuses the sim in output/.
  - `--reuse` re-mixes over `<name>_silent.mp4`. Rebuild it first with `ffmpeg -i <name>.mp4 -an -c:v copy <name>_silent.mp4`.
- Cost: sim about 3 min; Full HD render about 9 min at 2 encoder threads.
- Delivered <VIDEOS_DIR>\batch47\press_squeeze.mp4 (Full HD; v2 overwrote v1). Owner review: pending.

Owner review (2026-10-23): v2 "ok, we can publish; if it gets views it has room for a sequel" -> 4K + schedule.
- Owner review (2026-10-23): "ok this is something we can publish; if it gets views it has room for a sequel" -> APPROVED.
- **4K ship render** (2026-10-23, v7 sim cache, no changes): `output/press_squeeze_ship_9x16.mp4`, h264 yuv420p 2160x3840 60 fps, 16.62 s (997 frames), 43 MB. −14.01 LUFS, peak −8.81 dBFS, last 0.5 s silent, seam 2.12 (the genuine first-frame step), flash_check 0 = PASS. Notes and events match the Full HD.

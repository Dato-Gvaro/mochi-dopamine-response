# press_twin_hammer — REMATCH 2: Bolt brought TWO hammers

- Brief: docs/BRIEF_batch52.md (press franchise; press_split2 229K, press_split4 41.6K, press_squeeze 24.9K).
- Copied from scenes/press_split4.py (which stays bit-reproducible). **THE ONE CHANGE: Bolt's chamber has two drop hammers side by side** instead of one.
  - Hammer 1 walks the left half of the chamber, hammer 2 the right half (ping-pong, starting at the inner end so both first land on the shoulders of the one big ball).
  - Hammer 2 lands `--offset` s after hammer 1, so the blows alternate. Every blow spends only its own budget on the balls nearest ITS head (`pmask`: a ball already due from one head's blow is not counted again by the other).
  - `--winch own` (default): each head has its own winch. `--winch shared`: one winch's power split between the heads lifting at once.
- Unchanged: the press (full-width plate, pressure through the whole pile, ×3 waves), the look, jars, MAX line, Für Elise note per crush, banners, characters, overflow finale, dissolve loop, `post_fade`, 2-thread encoder.
- Drawing: one housing, two rods, two heads; label "2 DROP HAMMERS"; banners "PRESS WINS!" / "HAMMERS WIN!". Bolt's determined face for the first 2.4 s, then moods follow the honest lead.
- Sound: press_split4's, with each slam/latch panned from its own head; slam thunk 0.3 at gain 0.32 × m^0.3.

## v2 (default, 2026-10-27): Bolt SPLIT his hammer into two HALF-weight hammers

- Coordinator, after v1's blowout: same total mass as press_split2's single hammer, press_split4's honest mass rules per head with **m = 0.5** (`--mass`, default 0.5):
  - crush budget ×0.5 per blow; lift speed ×2 (5200 px/s, same winch, half the weight); free fall unchanged;
  - head area ×0.5: 80 × 54 px (half-width 58·m^0.534, height 74·m^0.463), rod half-width 9.9; housing unchanged so the drop is unchanged;
  - dust cushion ×0.5 (DUST_BED 7).
  - Gold "½" on each head. Caption: "Every ball ~CRUSHED~ splits / into 3 ~SMALLER~ ones / REMATCH 2: Bolt split his hammer in ~TWO~".
- **Search: the PRESS wins every run** (48 runs), always by its last ×3 wave (2187 → 6561), with ONE lead change at 23.3–23.8 s sim time (the last ~8 % of the race). Margin = hammer pile's distance under MAX at the press's overflow:

  | Seed | off 0.24 | off 0.30 | off 0.36 | off 0.45 |
  |---|---|---|---|---|
  | 0 | 177 | 148 | 114 | 121 |
  | 1 | 267 | 284 | 286 | 195 |
  | 2 | 151 | 102 | 156 | 135 |
  | 3 | 150 | 126 | 84 | 106 |
  | 4 | 156 | 274 | 131 | 95 |
  | 5 | 109 | 85 | **60** | 130 |
  | 6 | 169 | 210 | 156 | 120 |
  | 7 | 85 | 110 | 118 | 134 |
  | 8 | 218 | **75** | 238 | 164 |
  | 9 | 106 | 95 | 133 | 89 |
  | 10 | 259 | 148 | 199 | 90 |
  | 11 | 94 | 124 | 133 | 78 |

  Press overflow at 24.20–24.63 s sim time in every run (the press does not depend on the hammers).
- **Chosen: seed 8, offset 0.30** (0.30 s ≈ half the half-hammer's 0.6 s cycle). Seed 5 / 0.36 had the smallest final margin (60 px) but hammer 1's first blow misses the ball (Bolt reads 1 until 0.52 s); seed 8 / 0.30 lands both first blows (0.17 / 0.48 s).
- **The real closeness:** the hammer pile peaks **8 px under MAX at 23.38 s**, 0.34 s before the press overflows (the 75 px is after the pile settles at the press's overflow frame).

### Timeline (clip time, seed 8, offset 0.30)

- 0 s: 1 ball each, plate descending, hammer 1 falling, hammer 2 latched; Bolt determined. 0.17 s hammer split, 0.18 s press split; 0.48 s hammer 2.
- Counts M/B: 0.5 s 3/5 · 1 s 3/7 · 2 s 3/17 · 5 s 9/169 · 8 s 27/965 · 12 s 81/2,353 · 16 s 243/3,463 · 20 s 2,181/3,971 · 22 s 2,187/4,235.
- Press strokes at 0.17, 2.75, 6.40, 9.93, 13.33, 16.55, 19.67, 22.38 s.
- **22.98 s LEAD CHANGE** (press 4,441 vs 4,391, mid-wave). Hammer pile 8 px under MAX at 23.38 s.
- **23.72 s: the PRESS overflows** (6,561; hammers 4,515). Plate snaps and the pile erupts at 24.12 s, "PRESS WINS!". Bolt wow → annoyed; Mochi cheers + laughs.
- Dissolve 24.93 → 25.53 s; clip 25.53 s (1532 frames).
- Hammer slams/s: 3 4 2 4 4 2 4 4 3 4 4 4 4 4 4 6 4 5 5 5 6 5 7 6 (climbing). Hammer crushes/s: 3 5 3 18 43 89 130 191 98 199 214 183 190 123 104 134 91 56 38 73 70 62 78 78 121. Press crushes per wave: 3, 9, 27, 81, 243, 729, 2187 (≈1,127 + 1,060 in the last 2 s).

### Checks (encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch52\press_twin_hammer.mp4, v2)

- h264 yuv420p 1080x1920 60 fps, 1532 frames = 25.53 s.
- −13.99 LUFS, peak −6.5 dBFS. RMS/s −16.4 −16.8 −16.6 −16.7 −18.2 −16.5 −15.8 −16.1 −15.9 −16.2 −15.4 −15.7 −16.3 −15.8 −15.8 −15.4 −15.4 −15.4 −15.4 −15.3 −15.5 −15.2 −15.3 −15.4 −15.5, then −23.8 (dissolve). Last 0.5 s −24.8 dB, last 0.1 s −58.8 dB.
- Notes 116 (9 distinct), notes/s 3 4 3 3 3 3 6 6 4 3 4 3 4 5 2 5 7 5 3 7 4 4 11 7 5.
- flash_check 0 flashes = PASS (mean lum 0.033). Seam mean delta 0.84.
- Encoded frames read at 0, 0.5, 2, 23.0 (lead change), 23.38 (1:1 crop: pile at MAX by the left head), 23.75, 24.2 (finale), 25.5 s.

### Doubts (v2)

- The press wins in all 48 runs: the result is honest but it is the franchise's third press win. Framed as the running joke ("and STILL lost").
- Loudest momentary −13.0 LUFS at 9.5 s, not the finale (same as the predecessors).
- Hammer crush rate eases after ~11 s (shorter drops into dust); the slam rate and the press's waves keep climbing.
- The "½" badge is small (40 px font on an 80 px head).

## v1 (2026-10-27, superseded): two FULL press_split2 hammers — a blowout

- Reach it with `--mass 1.0 --offset 0.36 --seed 3` (caption switches to "REMATCH 2: Bolt brought ~TWO hammers~", heads numbered 1 / 2).
- Each head = press_split2's (mass ×1, 116 × 74, 2600 px/s lift, full budget, 14-grain cushion).
- `--winch own`, seeds 0-11: **the hammers overflow first in every seed**, at 13.4-17.3 s sim time, with the press on 81-721 balls and 406-508 px under MAX; no lead change. `--winch shared`: still a hammer win every time, 13.5-18.6 s (closest: seed 2, press 729, 355 px under).
- Why: one press_split2 hammer was 34 px short at 24 s; two give ~2× the crush energy per second and reach MAX ~8 s before the press's last waves.
- Seed 3 render: hammers overflow at 16.47 s clip time (5,617 vs 243), clip 18.28 s; −14.01 LUFS, flash 0, seam 0.92. Rejected by the coordinator: a foregone blowout breaks the owner's "outcome must not be obvious" rule.

## Args and cost

- Args: `--seed` (8), `--mass` (0.5; 1.0 = v1), `--offset` (0.30), `--winch` own|shared, `--cache` (pickles the sim in output/), `--label`, `--cap`, `--still --frame a,b`, `--report`, `--search A B`, `--reuse`.
- Cost: sim ~15-25 s per seed; Full HD render ~12 min at 2 encoder threads.
- Delivered <VIDEOS_DIR>\MochiAndBolt\review\batch52\press_twin_hammer.mp4 (Full HD, v2 overwrote v1). Owner review: pending.

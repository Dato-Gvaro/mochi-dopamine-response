# press_split4 — THE REMATCH: Bolt made his hammer HEAVIER (×1.3)

- **THE ONE CHANGE: the drop hammer is heavier.**
  - Default mass ×1.3 (`--mass`, default 1.3); `--mass 2.0 --seed 5` is the ×2 blowout.
  - Everything else is press_split2, the 2026-10-17 breakout (38K views in under 24 h, 77.6 % stayed): the rule, the press, the look, the characters, the counters, the Für Elise note per crush, the banners, the overflow finale and the dissolve loop.
  - press_split2 stays bit-reproducible; this is a new file.
- **Honest consequences of the mass factor m** (press_split energy-budget model), and nothing else:
  - Crush budget per blow ×m: `budget = m × E_K × (drop + E_BASE) × 100`.
  - Free fall is unchanged (gravity does not care about mass).
  - Lift speed ×1/m (same winch power): `H_UP = 2600 / m`.
  - The dust cushion needed to stop the head ×m: `DUST_BED = round(14 m)`.
  - The head's area ×m: half-width `58 m^0.534`, height `74 m^0.463`, rod half-width `13 m^0.386`.
    - ×1.3: 133 × 84 px.
    - ×2: 168 × 102 px.
  - The hammer's top housing is slimmed so the rest height, and therefore the drop, is unchanged.
  - The head has steel bands and a gold badge showing the actual factor ("×1.3").
- Caption: "Every ball ~CRUSHED~ splits / into 3 ~SMALLER~ ones / REMATCH: the hammer is now ~1.3× HEAVIER~". The factor is filled in from `--mass`.
- Bolt wears a determined face (brows down, flat mouth) for the first 2.4 s of sim time. After that, the moods follow whoever honestly leads.
- Sound:
  - The slam thunk is heavier (0.7 size, gain 0.40; was 0.3 / 0.32).
  - The riser leads into the winner's last machine hit.
  - **Post-master fade:** the mastering limiter swallowed the pre-master 0.6 s bed fade, because the loser hammer keeps slamming through the finale (the last 0.1 s measured -9.6 dB). `post_fade()` fades the MASTERED wav over the dissolve and re-muxes it with `-c:v copy` and no `-shortest`.
- Encoder: a scene-local `run_render_cool` caps ffmpeg at 2 threads (shared laptop).
- LEAD CHANGE banners may start up to 0.5 s before the overflow (press_split2 allowed 0.8 s), so the late lead change shows. OVERFLOW! still cuts it off.

## Search (2026-10-17)

- **×2: a blowout in every seed (0-11).** The hammer overflows at 16.4-20.6 s with the press on 243-995 balls, and there is no lead change. press_split2's hammer was already 34 px from MAX when it lost, so any big honest gain flips the result.
- Mass × seed grid (seeds 0-3). Winner, with the loser's margin under MAX:

  | Mass | Seed 0 | Seed 1 | Seed 2 | Seed 3 |
  |---|---|---|---|---|
  | ×1.1 | press, 59 px | press, 109 px | press, 86 px | hammer at 24.13 s, 0.3 s after the press's lead change, 162 px |
  | ×1.2 | press, 45 px | press, 37 px | hammer at 23.0 s, 183 px | hammer at 23.5 s, 179 px |
  | ×1.3 | hammer at 22.4 s | **press by 19 px** | hammer at 23.9 s, 0.1 s after the lead change | hammer at 21.95 s, no lead change |
  | ×1.4 | hammer at 21.6-22.0 s, 128-183 px; mostly no lead change | | | |

- **Chosen: ×1.3, seed 1, the closest finish of the grid.** The hammer leads the whole race, the press triples into the lead, and then it overflows with the hammer pile 19 px under MAX (press_split2: 34 px). In clip time:
  - Hammer's first split at 0.17 s; both counters read 3 by 0.3 s.
  - Counts M/B (press/hammer):

    | Time | Press | Hammer |
    |---|---|---|
    | 4 s | 9 | 41 |
    | 10 s | 27 | 1,409 |
    | 16 s | 243 | 3,021 |
    | 20 s | 729 | 4,289 |
    | 22 s | 2,187 | 4,641 |

  - **LEAD CHANGE at 22.93 s:** the press's last wave goes 2,187 → 6,561.
  - **The PRESS overflows at 23.60 s** with 6,561 balls. The hammer pile is 19 px under MAX with 5,229 balls.
  - The plate snaps and the pile erupts at 24.0 s ("PRESS WINS!").
  - Bolt shows "wow", then annoyed; Mochi cheers and laughs.
  - The dissolve runs from 24.82 s. Clip length 25.42 s (1525 frames).
- **Checks** (encoded Full HD):
  - Video: h264 yuv420p 1080x1920 60 fps.
  - Loudness: -14.02 LUFS, peak -4.8 dBFS.
  - Tail: last 0.2 s -24 dB, last 0.1 s -35 dB, last 50 ms -49 dB.
  - Seam mean delta 1.56. A normal frame step at the start is 1.36-1.40 (the head is falling), and the last frame is the sim frame just before frame 0.
  - flash_check: 1 flash = PASS (mean luminance 0.051).
  - Notes: 72 (9 distinct); per 5 s: 7, 15, 11, 18, 21.
  - Encoded frames read at 0, 0.3, 1, 3, 12, 22.95 (lead change), 23.3, 23.7 (overflow), 24.0, 24.4, 24.9 and 25.4 s, plus 1:1 crops of the finish and the faces.
- Nits:
  - The hammer keeps hammering after the overflow, so its pile creeps toward MAX during the eruption (5,229 → 5,539). That is honest, and the same as in press_split2.
  - The eruption sprays balls over the caption for about 1 s.
  - The notes per 5 s dip in the second window (15 → 11), before the press's waves take over.
- Cost: sim about 4 min; Full HD render about 12 min at 2 encoder threads.
- Args: `--mass` (1.3), `--seed` (1), `--label`, `--cap` (`{M}` = the factor), `--still --frame a,b`, `--report`, `--search A B`.
- Delivered <VIDEOS_DIR>\batch41\press_split4.mp4 (Full HD; it replaces the ×2 cut). Owner review: pending.
- Owner review (2026-10-21): press_split2 is at 112K views. The ×1.3 cut is green-lit to ship.
- **Side safe zone pass for the ship render** (measured on a tall phone, 2026-10-18; key elements inside x 0.10w–0.84w):
  - The sim and its logical geometry are untouched (same race, same timing). Only the stage drawing is scaled ×0.815 about the safe-zone centre (x 0.47w).
  - Walls now run x 110–905; the chamber top sits at y 475 and the floor at y 1290 (0.672 h).
  - Caption: centred at 0.47w, max width 789, lines at y 196, 272 and 342.
  - Banners: centred at 0.47w, y 900.
  - Counters: max width 360 at y 1482 (0.772 h). Labels are 30 px at y 1398.
  - Faces sit at 0.47w ± 37.5 between the labels.
  - Measured on a Fast still: the caption spans 0.107–0.835 w, and the stage plus HUD reach 0.839 w at the right. Only the eruption shards fly wider (decoration).
  - Frame 0 is still mid-action: the first splits land at 0.17 s.
- **Ship render** `output/press_split4_ship_9x16.mp4` (4K, `--label ship`, 9:16 only):
  - Video: h264 yuv420p 2160x3840, 60 fps, 25.42 s.
  - Loudness: -14.02 LUFS, peak -4.8 dBFS.
  - Tail: last 0.1 s -35 dB, last 50 ms -49 dB.
  - Seam mean delta 0.96.
  - flash_check: 0 flashes = PASS.
  - Measured x-range on the encoded frames:
    - Caption 0.107–0.836 w.
    - Stage 0.098–0.844 w, which includes the walls' neon glow. The walls themselves sit at 0.102–0.838 w.
    - Counters, labels and faces 0.128–0.812 w.
    - The eruption shards and sparks (decoration) reach 0.007 w at 24.1 s.

Owner review (2026-10-18): dropped.

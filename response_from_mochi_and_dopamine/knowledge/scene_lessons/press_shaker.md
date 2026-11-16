# press_shaker — THE PRESS vs a PAINT SHAKER: every ball hit HARD splits into 3, whose jar OVERFLOWS first? (batch64, 2026-11-01)

- Brief: docs/BRIEF_batch64.md (Mochi & Bolt 1, press franchise episode; **owner's call** — franchise episode vs the "never duplicate press_split2" rule; schedule ≥ Nov 7, away from `ol_brazil_nut`).
- New file copied from scenes/press_split4.py (which stays bit-reproducible). lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch64\press_shaker.mp4` (**v1**, Full HD 9:16, label v1).
- Caption (baked, 3 lines as press_tools): "Every ball hit ~HARD~ splits into 3" / "~Press~ or ~Shaker~:" / "whose jar ~OVERFLOWS~ first?" (Press coral, Shaker cyan, OVERFLOWS red, HARD gold).

## THE ONE CHANGE
- Bolt's drop hammer → a PAINT SHAKER: his chamber sits in a cradle (motor box "11 SHAKES / s", side clamp rods, bottom cradle plate on rubber feet, motion ticks) shaking y = A sin(2π·11 t), stroke 12 mm (A = 1.84 px at the franchise's 306 px/m = G 3000 px/s² ÷ 9.81): peak floor speed 0.41 m/s, ~2.9 g.
- Everything else is press_split4 seed 1: the press model, look, counters, faces, banners, Für Elise note per split, overflow finale, dissolve loop. The press race is bit-identical to press_split4 (same seed, chambers independent): 3 / 9 / 27 / 81 / 243 / 729 / 2,187 / 6,561, overflow at clip 23.60 s.

## Shaker physics (`Chamber.shaker_hits`)
- Same rule as the press: a ball splits into 3 (0.66× r) when hit hard. Hit = any contact (ball-ball, moving floor, moving lid, side walls) whose closing normal speed > V_BREAK(gen) = v0 × 1.155^gen, v0 = 0.62 m/s (gen 6 1.47, gen 7 1.70 m/s; dust immune).
  - Size effect: 1.155 per generation (0.66× radius) ≈ d^-0.35, inside the d^-0.25…-0.5 range of single-particle impact breakage (Tavares & King 1998). Brief said 1.12 (d^-0.25): with 1.12 the shaker grew steadily to ~4,700 and would overflow first at ~12 s (tested); 1.14 → ~2,400 by 22 s (lead change only 0.7 s before the overflow); 1.18 / 1.24 → stalls at ~120 / 57 for the whole race. 1.155 is the one that gives the brief's story honestly.
  - One split per ball per shake cycle (immunity = the cycle id, as the press's stroke id).
  - A fresh fragment's own burst is the breakage event, not a new hit: pieces younger than 0.15 s neither give nor take a hit (without this the franchise's split burst velocities chain-reacted to 2,400 pieces in 1.4 s).
- Damping is the franchise PBD's (contact damping 0.93/substep, dense-pile speed caps).
- Seed 1, clip times: shaker first split 0.10 s sim (pre-roll), 69 balls at 0.5 s, 101 at 1.4, then a crawl 115-123 (2-5 s), 155 (7.4), 213 (11.4), 313 (15.4), lead change at 16.52 s (press 243 → 729 vs shaker ~340), shaker 537 (19.4), 675 (21.4), 799 at the overflow. The press overflows at 23.60 s → "PRESS WINS!". Shaker leads 0.1-16.5 s (65 % of the clip); lead change 7.1 s before the overflow.

## Nerd stats
- Bolt's chamber: "SMALLEST PIECES: 95% OF HITS < x m/s" (95th percentile of the hits the smallest breakable generation took, averaged over 0.5 s; 0.23-0.75 m/s all race) and "THEY BREAK ABOVE y m/s" (1.47 → 1.70); red "TOO SOFT" shown from 2.5 s (true from 0.5 s; hidden during the opening burst so it does not read as a contradiction). The rare 5 % tail still splits pieces — that is why the count crawls instead of freezing.
- Press housing: "1 SQUEEZE every ~3 s" (sim: 2.58-3.65 s, mean 3.2).
- Banner "HITS TOO SOFT FOR THE SMALL ONES" 3.1-4.9 s. Franchise LEAD CHANGE / OVERFLOW / PRESS WINS banners.
- Not built: the brief's "PRESSURE gauge" (press_split4 has none); Bolt riding the motor box (faces stay in the franchise HUD spots; "faces never shake").

## Sound
- Für Elise note per split (merged ≤1/60 ms), franchise crunch per split, press thunk/hiss, A-minor cadence on the overflow, riser into the final stroke — all press_split4.
- Shaker: a quiet tonal clamp tick per shake (165 Hz, 0.05 s, gain 0.035) and a low tonal motor hum (55 + 110 Hz, pulsing at 11 Hz, gain 0.03). No noise bed.
- post_fade changed: the mastered wav is now faded to silence by 0.5 s before the end (press_split4 left -35 dB in its last 0.1 s).

## Args
- `--seed` (1), `--v0` (0.62), `--grow` (1.155), `--stroke` (0.012), `--freq` (11), `--fresh` (0.15), `--resim`, `--still --frame a,b`, `--report`, `--reuse`, `--label`. The sim is cached in `output/press_shaker_sim_s1_v0.62_g1.155_a0.012_f11.pkl` (~6 min to rebuild).

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 1525 frames = 25.42 s. Muxed -14.01 LUFS, peak -6.41 dBFS, last 0.5 s -240 dBFS (silent).
- flash_check PASS (0). Seam mean |delta| 1.24 (mid-action dissolve into the pre-roll; press_split4 shipped at 1.56).
- Notes 156 (9 distinct, top 17 %); events/5 s 20 / 18 / 25 / 40 / 53 (climbing). RMS/5 s -16.0 / -25.1 / -16.6 / -19.1 / -15.6: the 5-10 s window is quiet (the shaker crawls, the press is between strokes) — owner to judge.
- Side safe zone: the press_split4 stage transform (walls 110-905); cradle rods/feet/motion ticks reach ~0.85-0.86w (decoration); text inside 0.10-0.84w.
- Frames read from the mp4: 0.03, 0.3, 1.5, 4.0, 12.0, 16.6 (lead change), 23.0, 23.7 (overflow), 24.3 (PRESS WINS); stills at 0.5, 3.3, 11.7, 16.9, 23.8.

## Outcome
- (fill after upload)

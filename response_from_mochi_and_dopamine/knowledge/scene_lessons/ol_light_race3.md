# ol_light_race3 (DopamineEXE, owner review docs/REVIEW_1114.md)
- v3 of `ol_light_race2` (v2 untouched). Owner 2026-11-14: "the jet and the car start too fast"; ">> 10X" is not readable, use "FAST FORWARD ×10" with the ⏩ icon.

## What changed vs v2
- **Diagnosis:** with pure ×10 steps, lane speed (710 px lane) jumps 10x per step. The jet's and car's lifetimes (17.8 / 160 days) sit just above a power of ten, so their runs played at 462 / 513 px/s: about 2x the rocket's (260), walker's (256) and snail's (185). In v2 each ran its lane in about 1.4 s.
- **Fix: two ×3 half-steps** in the ladder, ×300,000 for the jet and ×3 MILLION for the car.
  - Each now starts its run slowly: the jet crawls at 46 px/s under ×100,000 (during the rocket's run), then 138 px/s, then ×1 MILLION finishes it.
  - The car crawls at 51 px/s under ×1 MILLION, then 154 px/s, then ×10 MILLION.
  - The 10%-to-finish run is now 3.75 s for the jet (v2 1.42 s) and 2.72 s for the car (v2 1.39 s).
- **Every level is held ≥ MIN_HOLD 1.05 s** (asserted). Steps land on half beats (whole beats over-held the early badges).
  - The ×10/×100/×1,000 steps were 0.5 s apart in v2. They are now 1.08-1.30 s each.
- **The badge:** an 84 px pill with a drawn fast-forward icon (two filled triangles), "FAST FORWARD" at 40 px, then the multiplier at 58 px ("×10" … "×100 BILLION", with a real × sign).
  - It is fitted to 790 px, centred on x 505. Level 0 shows a single play triangle and "REAL SPEED".
  - The pop is 1.22x; the ghost ring is 1.32x.
- **Music tempo** is re-solved for the longer ladder: segment A 1.7 → 3.5 beats/s, segment B 3.5 → 5.6 (it accelerates). Clock ticks climb 3 → 8 per second.
- **Length:** 25.43 s (v2 21.62 s).
- The facts, stamps, counters, finale and loop dissolve are the same as v2.

## Ladder (`--dry`)
| level | step at (s) | held (s) |
|---|---|---|
| REAL SPEED | 0 | 1.44 (light lands 1.23) |
| ×10 | 1.44 | 1.11 |
| ×100 | 2.56 | 1.08 |
| ×1,000 | 3.64 | 1.30 |
| ×10,000 | 4.94 | 1.25 (rocket crawls) |
| ×100,000 | 6.19 | 3.04 (rocket run, lands 8.97; jet crawls) |
| ×300,000 | 9.23 | 1.30 (jet run starts) |
| ×1 MILLION | 10.53 | 1.24 (jet lands 11.53; car crawls) |
| ×3 MILLION | 11.77 | 1.38 (car run) |
| ×10 MILLION | 13.15 | 1.12 (car lands 14.10) |
| ×100 MILLION | 14.27 | 2.91 (walker lands 17.05) |
| ×1 BILLION | 17.18 | 1.09 |
| ×10 BILLION | 18.27 | 1.17 |
| ×100 BILLION | 19.44 | 3.90 (snail lands 23.34, gold 12,181 YEARS) |

## Knobs
`--tempo0 1.7 --tempo1 3.6` (`--dry` must print `accelerates: True`), `--jet-hold 1.3`, `--car-hold 1.2`.

## Open
- The opening (×10 to ×1,000, 1.4-4.9 s) is clock and counters only. That is the "start slow" the owner asked for in v2. At ≥1 s per badge it is 3.5 s.
- A literal visible crawl at REAL SPEED is impossible on a true-scale lane: 1 px = 541 km, and the jet covers 0.4 km in 1.7 s. The per-lane distance counters carry that crawl.

## Result
- FHD verified 2026-11-14: 25.45 s, -14.0 LUFS, peak -5.0 dBFS, flash PASS (0), seam 0.546. Review: `<VIDEOS_DIR>\DopamineExe
eview\ol_light_race3.mp4`.

## 4K fix (2026-11-14, shipper)
- First 4K render did NOT match the FHD (mean |Δ| 3.9, p99 99): `paint_art` painted the O.FX parts (Earth rim, Moon shading, glows) in the scaled ctx while their matrix already maps to DEVICE px, so at NF_SCALE 2 they drew at 2x. Fix: `paint_parts` under `ctx.identity_matrix()`. No-op at NF_SCALE 1 (FHD still vs approved video 0.39 = encode noise); 4K still vs FHD still 0.07.
- Any other scene that calls `LOOK.paint_parts` with `base` folded into the matrix has the same 4K trap.

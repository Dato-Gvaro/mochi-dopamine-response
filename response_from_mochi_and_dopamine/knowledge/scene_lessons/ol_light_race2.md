# ol_light_race2 (DopamineEXE, BRIEF_1113b B2) — CODE ONLY, not rendered yet
- v2 of `ol_light_race` (v1 untouched, still reproducible). Owner: rocket and jet far too fast → start slow at REAL speed, then visible ">> 10X / 100X" steps, then fast.
- File: `scenes/ol_light_race2.py`. Standalone (art from ol_domino_style_test2 / ol_domino3_objects / ol_domino_giant, read-only, as v1).
- Review folder (later): `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_light_race2\`.

## What changed vs v1
- **Warp ladder** replaces v1's continuous ×1→×100 BILLION ramp. Level k = exactly ×10^k, each step on a whole music beat, eased 0.3 s in log space.
  - Level 0 = REAL SPEED for 1.71 s. Light crosses in its true 1.28 s (pre-roll 0.05 s, lands at 1.23 s).
  - Steps: ">> 10X" … ">> 100 BILLION X". The pill swaps label with a pop + a ring-out ghost. Chevrons run faster each level. A soft upward sine "zip" SFX on each step.
  - Every racer's 10%→finish run lasts ≥1.15 s (rocket 2.46, jet 2.84, car 1.68, walk 2.49, snail 3.46). v1: rocket and jet were ~0.7 s apart.
- **Per-lane distance counters** (new) show the crawl at real speed: rocket 1.8 km, car 36 m, snail 1.3 mm when light lands. Each counter becomes the gold/white stamp on arrival.
- **Speed streaks** behind a racer whose lane speed is >60 px/s (more streak as the warp rises).
- **Clock**: live at real speed; from the first step it ticks on melody notes and never lags an arrival (it shows the exact true time on the arrival frame). Days show 1 decimal under 100 (17.8 DAYS = the jet stamp).
- **Music**: Grieg, Mountain King (Mutopia 1888), now from the theme's first note (beat 4) to the B-minor tonic (beat 68).
  - Segment A: exponential tempo 1.7 → 4.23 b/s up to the last step (beat 48).
  - Segment B: a linear ramp 4.23 → 6.07 b/s, solved so beat 68 = the snail's arrival.
  - Bassoon until the rocket lands, then strings; horns from the walker; timpani from the car. Finale chord as v1.
- The facts, stamps, caption, finale, layout and loop dissolve are as v1. The clock moved up 30 px (y 470) and the pill sits at y 500-556.

## Rung table (from `--dry` + math, defaults `--tempo0 1.7 --tempo1 4.6`)
| clip s (frame) | on screen | clock / warp |
|---|---|---|
| 0.00 (0) | Light already streaking (4%); everyone else on the line; counters 70 m / 1.4 m / 0.1 mm; pill REAL SPEED | 0.05 s, ×1 |
| 1.23 (74) | **LIGHT lands** (stamp 1.28 SECONDS, ring); others still at 0% (rocket 1.8 km, car 36 m, snail 1.3 mm) | 1.28 s |
| 1.71 (103) | **>> 10X** badge | 1.8 s |
| 2.79 (168) | **>> 100X** | 11 s |
| 3.83 (230) | **>> 1,000X** | 1.6 min |
| 4.83 (290) | **>> 10,000X**: the rocket starts to creep (0.3%) | 15 min |
| 5.79 (347) | **>> 100,000X**: the rocket's run (3% → 100% in 2.8 s), jet creeping | 2.4 h |
| 8.60 (516) | **ROCKET lands** (3 DAYS 4 HOURS); jet at 18% | 3.2 days |
| 8.84 (530) | **>> 1 MILLION X**: the jet's run | 3.4 days |
| 10.25 (615) | **JET lands** (17.8 DAYS); car at 11% | 17.8 days |
| 10.39 (623) | **>> 10 MILLION X**: the car's run | 19 days |
| 11.78 (707) | **CAR lands** (160 DAYS); walker at 5% | 160 days |
| 12.16 (730) | **>> 100 MILLION X**: the walker's run | 204 days |
| 14.92 (895) | **WALKING lands** (8.8 YEARS) | 8.8 years |
| 15.20 (912) | **>> 1 BILLION X** (snail 0.1%) | 9.6 years |
| 15.99 (959) | **>> 10 BILLION X** (the snail starts to creep) | 29 years |
| 16.98 (1019) | **>> 100 BILLION X**: the snail's run (2.4% → 100% in 3.9 s), clock spinning through centuries | 287 years |
| 20.90 (1254) | **SNAIL lands** on the B-minor tonic: gold clock 12,181 YEARS / THE SNAIL ARRIVES, timpani + boom | 12,181 years |
| 20.9-22.4 | complete state: all 6 lanes full, 6 stamps | |
| 22.4-23.0 | 0.6 s dissolve to frame 0 (loop) | |

- RENDERED 2026-11-13: x10/x100/x1,000 cut to 1 beat each, late holds 4/6 beats, tempo 1.8/5.2, the opening theme lifted +12. FHD **21.62 s**, -14.0 LUFS, flash PASS, seam 0.544. The table above is the pre-render plan; the final timeline is in the review README.
- Planned length was 23.00 s; v1 was 14.23 s.
- Seconds per level: 1.71 / 1.08 / 1.04 / 1.00 / 0.96 / 3.05 / 1.55 / 1.77 / 3.03 / 0.79 / 0.99 / 3.93.
- Clock ticks/s climb roughly 3 → 9. There is a dip to 1 at ~7 s (a rest in the score; v1 had it too).

## Knobs
- `--tempo0` / `--tempo1`: segment-A tempo. 1.7 / 4.6 is the only tested pair where segment B still accelerates. Check `--dry` prints `accelerates: True`.
- `LADDER` in the file: the hold per level (`beats` n) or "step 0.3 beat after racer i lands" (`after`).

## READY TO RENDER (later pass; render lock for clips, not for stills; TEMP/TMP on D:)
```powershell
$env:TEMP='<REPO>\output\tmp'; $env:TMP=$env:TEMP
python scenes/ol_light_race2.py --dry                                   # expect clip 23.00s, 1380 frames
$env:NF_SCALE='1.0'; $env:NF_FAST='1'
python scenes/ol_light_race2.py --still --frame 0,74,110,350,520,700,1030,1260,1370 --label t
# then (lock: mkdir output/render.lock ... rmdir)
python scenes/ol_light_race2.py --label fast                            # FAST clip, verify
Remove-Item Env:NF_FAST
python scenes/ol_light_race2.py --label fhd                             # FHD (NF_SCALE=1.0)
python tools/flash_check.py output/ol_light_race2_fhd_9x16.mp4
```
- **Stills, what to check:**
  - f0: light streaking at 4%; the distance counters are readable and do not touch the lane names (JUMBO JET + pace ends ~x 430; counters are right-aligned at x 838).
  - f74: the light stamp; the other counters show the crawl.
  - f110: the 10X badge ghost ring. Must not hit the clock (clock baseline y 470, ghost up to ±53 px around y 528).
  - f350 / f520 / f700: rocket, jet and car runs. Speed streaks behind the moving racer only, nothing behind parked racers.
  - f1030: the snail run under "100 BILLION X". The pill is the widest here (~360 px; ×1.9 ghost ≈ x 167-843, inside 0.10-0.84w).
  - f1260: gold finale. f1370: the dissolve.
  - Side safe zone: all labels inside x 108-907 (MOON label right edge 900).
- **Clip checks:** onsets (warp zips, arrival dings, ticks), -14 LUFS on the muxed mp4, tail silent, flash_check PASS (the badge ghost is a thin ring, not a flash), loop seam.
- **Owner-facing:** v1 README facts/sources/titles still apply. Title idea: "Light takes 1.3 seconds. The snail takes 12,181 YEARS 🐌".

## Open risks
- No frame has been drawn yet (code-only pass). The new draw code is `draw_pill`/`chevrons`/`speed_lines`/the distance counter; a first still may need spacing tweaks.
- 23 s is 60% longer than v1. The 4 badge steps before the rocket moves (1.7-5.8 s) have only the clock, counters and badges moving. That is the "start slow" the owner asked for, but check the stay curve against v1's.
- The ×100,000 and ×100 BILLION levels are ~3-4 s long. They are readable runs, not padding, but they are the longest single rungs.
- The Grieg excerpt now starts at the low theme (beat 4, transposed +12 like v1). Listen for "creepy" low register at real speed. If it is, start at beat 20 (v1's start) and re-tune the tempi.

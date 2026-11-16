# ol_earths_in_sun2 (DopamineEXE, BRIEF_1113b C1; rebuild of ol_earths_in_sun)
- Owner 2026-11-13: idea OK; the camera cuts/skips must be smooth. v1 file untouched (bit-reproducible).
- Facts, sound, HUD, clock, finale = v1 (see `ol_earths_in_sun.md` + the v1 review README). Only the camera and LOD changed.
- Status 2026-11-13: CODE ONLY (owner on the laptop). `--dry` smoke run passes; nothing rendered yet.

## Where v1 skipped (found in the code)
| v1 source | effect on screen | v2 fix |
|---|---|---|
| `Cam` zoom from `ext_of(int(n))` = the cumulative-max STAIRCASE of the pile size | a zoom jump on landings; measured on v1's camera: one-frame jumps of ln s 0.45 at 0.87 s (scale ×0.64 in ONE frame), 0.28 at 1.90 s, 0.18 at 2.32 s, 0.14 at 3.27 s, 0.21 at 4.88 s, 0.15 at 5.57 s | continuous n (`ext_cont`), monotone, Gaussian-smoothed ln s (sigma 0.30 s) in `simulate()` |
| target weight w from that s | the framing slid in steps with each zoom jump | target computed from the smoothed s |
| sprite radius quantised to 2 px above 20 px, integer-pixel blits | big Earths changed size in 2 px steps and stuttered 1 px on the slow camera | ~2% steps below 20 px; above 20 px exact scale + sub-pixel position |
| detailed/dot LOD switch at 4 device px (= 2 px at 4K, 4 px at FHD) | every Earth popped style at once | crossfade dot -> detailed over 3.6-6.0 logical px (t ≈ 7.1-9.3 s) |
| continents 3 -> 5 at r 12 px, clouds on at r 9 px | texture pop on every Earth | always 5 continents; clouds fade in over 4-10 px |
| falling Earths re-picked by `linspace(…, 700)` every frame | falling Earths flickered/jumped (a new subset each frame) | stable per-site hash < p with an alpha margin |
| fall start height switched at s = 12 | every falling Earth jumped mid-air | blend over s 16 -> 9 |
| `hot` gold tint in 8 steps, linear | slight step at the finale | 16 steps, smoothstep |

## Camera continuity (asserted in `simulate()`, every drawn frame incl. the loop dissolve)
- Limits: |d ln s| <= 0.030/frame, |d2 ln s| <= 0.0030, target screen motion <= 14 px/frame, never zooms back in.
- Measured (`--dry`): max |d ln s| 0.0134 at 3.68 s, max |d2 ln s| 0.00037, target 2.9 px/frame, Earth #1 max 1.2 px/frame in 0-4 s. s 108.4 -> 3.30 px/R (S_F 3.28). All of the first 256 landings land inside the content area (y 330-1175).
- The camera starts its pull-back ~0.3 s before Earth #1 lands (non-causal smoothing = anticipation; intended).

## Rung table (clip second -> on screen -> count). Clock = v1.
| s | on screen | count | camera (px per Earth radius) |
|---|---|---|---|
| 0 | a big Earth already falling into the glowing bowl, lands 0.30 s | 1 | 108, pull-back starting |
| 1 | 2nd, then the 3rd/4th Earths land beside it | 2 -> 4 | 76 |
| 2 | a cluster | 8 -> 16 | 52 |
| 3 | a rain of Earths, camera pulling back steadily | 32 -> 64 | 31 |
| 4 | a heap on the Sun's floor, the bowl's curve visible | 128 -> 512 | 16 |
| 5 | the pour widens; "MORE THAN JUPITER (1,321)" at 5.76 s | 1,024 -> 1,321 | 11 |
| 6 | a flat layer across the bottom | 2,048 -> 4,096 | 8.2 |
| 7 | most of the Sun in view, ~1%; dot/detail crossfade begins | 8,192 -> 16,384 | 6.3 |
| 8 | whole Sun nearly in frame, 2.5% -> 5% | 32,768 -> 65,536 | 4.6 |
| 9 | the level climbs 10% -> 40% | 131,072 -> 524,288 | 3.8 |
| 10 | "1 MILLION EARTHS… ONLY 80%", FULL 10.15 s, ignition | 1,048,576 -> 1,304,000 | 3.34 (settled) |
| 11-12 | blazing Sun, final line, hold, dissolve to frame 0 | | 3.30 |
Length 12.70 s (762 frames), same as v1.

## READY TO RENDER (later, under the render lock; TEMP on D:)
```powershell
$env:TEMP='<REPO>\output\tmp'; $env:TMP=$env:TEMP
python scenes/ol_earths_in_sun2.py --dry                                   # asserts + timeline, ~1 s
$env:NF_FAST='1'; python scenes/ol_earths_in_sun2.py --still --frame 0,30,60,120,240,420,480,540,600,660; Remove-Item Env:NF_FAST
$env:NF_FAST='1'; python scenes/ol_earths_in_sun2.py --label fast; Remove-Item Env:NF_FAST     # full FAST clip
$env:NF_SCALE='1.0'; python scenes/ol_earths_in_sun2.py --label fhd; Remove-Item Env:NF_SCALE  # FHD (v1 took 70 s)
python tools/flash_check.py output/ol_earths_in_sun2_fhd_9x16.mp4
```
- Expected: 12.70 s, 762 frames, 1080x1920 @ 60 (FHD), -14 LUFS (sound = v1).
- Stills to read and what to look for:
  - 0 / 30 / 60 (0, 0.5, 1.0 s): Earth #1 framed under the caption; the 0.5 s frame must NOT show the v1 jump (in v1 the 0.5 s sheet frame had Earth #1 moved and a 2nd big Earth top-right).
  - 120 / 240 (2, 4 s): no Earth cut by the caption or the meter; continents look the same as at 0 s.
  - 420 / 480 / 540 (7, 8, 9 s): the dot/detail crossfade: no double-rim or ghost halo on the dots.
  - 600 / 660: FULL + ignition, as v1.
- On the FAST clip: scrub 0-5 s frame by frame (zoom must glide, no step), and 6-9 s for falling-Earth flicker.
- Copy to `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_earths_in_sun2\` with a contact sheet.

## Open risks
- Render time up in 7.1-9.3 s: two sprites per Earth during the LOD crossfade (tens of thousands of wall sprites).
- Exact-scale blits above 20 px use FILTER_GOOD bilinear: big Earths may look a touch softer than v1's 1:1 sprites.
- The smoothed camera leads the pile slightly (anticipation); if the owner wants the camera to "follow" more tightly, lower `--camsig` (0.30 s; the asserts still guard jumps).

## Result 2026-11-13 (FHD, label fhd)
- Still fix: Earth #1 frame-0 start 3.6 -> 2.9 R above its site (v1 height touched caption line 2).
- 12.70 s, -14.01 LUFS, -4.9 dBTP, flash 0, seam 0.405. Frame-step scan (max delta / neighbours): v2 2.9 (gold turn at FULL) vs v1 18.0 (0.87 s). FHD render ~1.5 min.

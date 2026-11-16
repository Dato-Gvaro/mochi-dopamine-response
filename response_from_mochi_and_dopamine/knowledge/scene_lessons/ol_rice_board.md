# ol_rice_board (Overflow Lab, channel 2)
- Character-free (docs/BRIEF_channel2.md). The wheat/rice-on-a-chessboard legend as physics. ×2 growth toward a named end state (owner 2026-10-21: "more math, splits, exponents, triangles").
- **v2 (current), doubling glass tubes**: a physical exponential bar chart.
- Caption (baked, `--cap`; `--cap ''` = base): `Every tube gets ^DOUBLE^ the last|until one ^OVERFLOWS^`. DOUBLE takes the current tube hue; OVERFLOWS is gold.
- Delivered: `<VIDEOS_DIR>\channel2\ol_rice_board.mp4` (v2, Full HD, seed 5, label fhd2, 14.38 s). No 4K yet.
- Owner review of v1 (2026-10-22): "good idea but something is off, maybe instead of a board use something else". v1 was a tilted board with pyramid-roof heaps; it is replaced by v2.

## v2 world (logical 1080x1920)
- **Tubes**: 11 identical clear glass tubes in a row, x 118-898, pitch 70.9.
  - Inner size 54 × 818 px; rim y 362, inner bottom y 1180.
  - Outline 2 px white at 72%, a rim lip, and a soft vertical sheen. Rounded bottom corners.
- **Shelf**: one white line at 85% (x 108-907) over a dark slab.
- **Goal from frame 0**: a dashed gold line at the rims, labelled "OVERFLOW" (right end, y 346).
- **Beads**: r 4.5 (drawn 4.75), glossy sprites. Hex packing in the tube, layers alternating 6 / 5 beads, layer pitch 7.79 px. **Every bead is one grain**; the legend reads "● = 1 grain".
  - The fill height is the honest packing of the true count: 1.42 px per grain on average.
  - Tube capacity is 572 grains: tube 10 (512) stands at 88% of the glass, tube 11 (1,024) cannot fit.
- **Colour rule**: one ordered hue ramp across the tubes, cyan 0.50 → azure → blue-violet → violet → magenta 0.86, at S 0.75 / V 1.
  - Only the shade (4 levels) varies per bead; no random hues.
  - Gold is the one warm accent: the OVERFLOW line and mark, tube 11's rim glow, every 9th geyser bead, the ×2 pill after the overflow, the race notches on the meter, and the final number and line.
- **Labels**: each tube's live count rides the top of its column ("1, 2, 4 … 512, 575"); the exponent 2⁰ … 2¹⁰ sits under the shelf.
- **HUD**:
  - Meter y 1290: 64 notches with "TUBE n / 64", the gold OVERFLOW mark at 10.56/64 (tube 11 at 572 of 1,024) and "64" at the end.
  - Counter y 1482 (true grains), ×2 pill, "GRAINS".
  - Watermark at (900 right, 1366).
  - Final overlay at y 560 / 634: "64 TUBES = 2⁶⁴ − 1" / "18 QUINTILLION GRAINS".

## v2 clock and physics
- Every grain falls from y 334 (v0 900, g 3000) into its slot, bottom layer first, in random order inside a layer.
- **Tubes 1-8**: tube n lands at 0.10 + 0.235(n−1) s (one tube per 8th note), its grains spread over 0.17 s. A tint pop on the glass and a ×2 pop on each.
- **Tubes 9-11**: one exponentially rising pour, rate r0·e^(0.2 t), r0 = 63.8/s.
  - Tube 9 starts at 2.00 s, tube 10 at 4.94 s, tube 11 at 8.12 s.
  - The first grain tube 11 cannot hold (#573) lands at **10.23 s = OVERFLOW**.
  - The rest of tube 11 gushes in at 900/s; the counter stops at the true 2,047 at 10.73 s.
- **Geyser**: every overflowing grain leaves the rim with vy −250…−800 px/s, 78% thrown left over the row (vx −60…−420) and the rest right (30…200).
  - g 2600, one damped bounce on the shelf (×0.32 vertically, ×0.7 horizontally), then off the shelf and down the frame.
  - While the counter races, the pour keeps gushing at 1,500/s (visual only; those grains are not counted). It stops 0.35 s after the race.
- **Race**: 10.88-12.43 s, tube 11 → 64 (accelerating), counter 2^k − 1 to **18,446,744,073,709,551,615**, which turns gold. Then a 1.35 s hold and a 0.6 s dissolve into the empty pre-roll. **14.38 s, 863 frames.**
- **Landings per second**: 15, 241, 71, 86, 106, 129, 158, 192, 236, 287, 929 (overflow), 1500, 1127.

## v2 on screen
- **0 s**: 11 empty tubes, the gold OVERFLOW line, tube 1 tinted, its grain falling.
- **0.5 s**: tubes 1-2 done ("1", "2", 2⁰ 2¹), tube 3's 4 grains falling, counter 2-3.
- **1 s**: 1 2 4 8 done, tube 5 raining, counter 15.
- **2 s**: tubes 1-8 standing as a curve, 1 … 128 (128 = 23 layers, 180 px), counter 255-256, tube 9 starts.
- **7 s**: tube 10 half full (806 grains).
- **10.23 s**: tube 11 hits the rim (575), gold glow, geyser.
- **11-12.4 s**: an avalanche over tubes 6-10 and the shelf, the counter racing.
- **12.4 s**: 18 QUINTILLION.

## v2 sound
- **Melody**: Schubert, Marche militaire No. 1 in D, D. 733/1 (PD). Mutopia "Mutopia-2008/09/28-1545"; files in `<SOUNDFONTS_DIR>\scores\schubert_marche_militaire1\` with `SOURCE_mutopia_1545.txt`.
  - Tubes 1-8 = the fanfare, bars 1-2 (one tube per 8th).
  - Tube 9 = 3 bars (bars 3, 5, 7), tube 10 = 4 bars (8-11), tube 11 = 3 bars (12-14) up to the overflow. Each tube starts on a downbeat. Bar lengths: 0.98 → 0.79 → 0.70 s.
  - Bar 14's rising scale lands on bar 15's A-major chord at the OVERFLOW.
  - Notes snap to a grain landing within 20 ms.
- **Arrangement** (as in v1):
  - The fanfare is doubled by horns and strings, with timpani on every beat and a boom on tube 1 (`--open` 2.6).
  - Strings carry the theme, celesta the top notes; contrabass and timpani on the downbeats; a timpani roll under bar 5; oohs swell into the arrival.
  - 38 celesta chimes on sampled landings, rising from 1 to 9 per second.
  - OVERFLOW: a rolled A-major chord with strings, horns, oohs, bass, timpani and a boom (`--fin` 5.5).
  - Race: a rising A-major harp and celesta line, one note per tube. Tube 64: a celesta/strings chime and timpani.
- **SFX**: a bead "tk" per grain landing (two tonal partials 1.6-3.0 kHz, 0.6-1.0 kHz body, nothing above 5.5 kHz), at least 12 ms apart, gain ÷ √(rate/10). 812 ticks.
- **Mastering**: `audio.master(peak_db=None, reverb=0.5)`, sfx ×0.30.
  - RMS per second: −20.6, −22.5, −21.6, −20.8, −19.5, −18.8, −17.9, −18.4, −16.9, −17.5, **−15.0, −15.0**, −16.0, −32.6, silence.
  - Finale 10.2-11.7 s: −14.6 dB vs the late body −17.5 (+2.9 dB). Lowest half-second before the finale: −22.8.

## v2 checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps, 863 frames.
- flash_check PASS (0 flashes, mean lum 0.012).
- −14.01 LUFS, peak −4.81 dBFS, last 0.5 s digital silence, energy above 6 kHz 0.095%.
- Seam mean |Δ| 0.346 (good band).
- Frames read from the mp4 at 0, 0.5, 1, 2, 7, 10.23, 10.83, 11.67, 12.67 s and the last frame. 1:1 crops of the geyser at tubes 9-11 and of the opening tubes 1-4.
- Geyser beads fly past x 0.84 w and over the caption; decoration only, the caption and HUD are drawn on top.

## v2 flags
- General: `--seed (5) --label --cap --still --frame a,b,c --dry --sound 0 --remux --sfx (0.30) --fin (5.5) --open (2.6)`.
- Clock: `--p1 (0.235) --k (0.20) --tbuild (8.25) --gush (900) --flood (1500) --trace (1.55) --hold (1.35)`. Look: `--rbd (4.75)`.
- The overflow is always grain 573 of tube 11. `--k` / `--tbuild` move its time; the beat map follows it automatically.

## v1 (superseded 2026-10-22; its code is replaced, parameters kept here)
- **Board**: an 8×8 glossy board under a 55° pinhole camera (focal 1800, distance 1700, Y0 812), squares 80 px, snake order from the near-left corner, hue 0.05·(n−1) at S .85.
- **Grains**:
  - Squares 1-8 were hex-cone bead piles, bead r 3.3 (drawn 3.6).
  - Squares 9+ were angle-of-repose cones (S_C 0.8) on a 5 px height field. VG = 0.82·d³ = 236 px³; each frame the cone's apex was bisected so the added volume matched the grains that landed. The heaps were capped by the edge roof S_C × distance to the edge.
  - Rolled-off grains made downhill streaks and spills.
- **Timing**:
  - Square durations from 9 on: 1.0, 1.08, 1.1, 1.08, 1.0, 0.94, 0.86, 0.78, 0.7, 0.64, then 0.58 … 0.42 s.
  - OVERFLOW (board 99.5% covered) at 11.17 s, at the end of square 18. Race 11.47-13.02 s. Total 14.97 s.
- **Checks**: flash 0, −14.01 LUFS, seam 0.234.
- **Flags**: `--rb 3.3 --vg 236 --sc 0.8 --fallh 150 --rbd 3.6 --pitch 55 --y0 812 --durs …`.

Owner review 3 (2026-10-22): "mixed feelings, it has potential to get better" -> hold (not in the first batch); revisit.

Owner review 4 (2026-10-22): "no opinion, if research thinks ok lets try" -> Dopamine.exe schedule.

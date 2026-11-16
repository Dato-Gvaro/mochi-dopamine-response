# growth_race3 — "Mochi CUBES it, Bolt DOUBLES it" / "whose tank fills first?" (batch68)

- Brief: docs/BRIEF_batch68.md §1 (owner on growth_race: "+100 vs x2 is lazy"). New file `scenes/growth_race3.py`; growth_race untouched. Built from growth_race's tanks/balls/spill code (same geometry: FULL = 2,048 balls, r 6, hex rows 29/28).
- Mochi = x³, Bolt = 2ˣ, x = 1..11; each tank always holds exactly its formula's value (Bolt starts with 2⁰ = 1 ball, Mochi 0³ = 0).
- Counts: x1 1/2 · x2 8/4 · x9 729/512 · **x10 1,000/1,024** · x11 1,331/**2,048 = FULL** · x12 (finale) 1,728/4,096 (2,048 spill over both rims).
- Kept the brief's default pair. x² vs 2ˣ was not used: it ties at x = 2 and x = 4 and Bolt leads from x = 5, a short lead for Mochi (rounds 3-4 only).

## Layout
- As growth_race. Hoppers labelled with the formula (x³ / 2ˣ, gold, exponent drawn small and raised). "x = n" replaces ROUND. Under each tank "CUBES n³" / "DOUBLES 2ⁿ" (size 40) and the exact count (gold = leader). "+N" pops under the hoppers (Mochi +3n²-3n+1, Bolt +2ⁿ⁻¹).
- x = 12 label flips 0.30 s AFTER FULL (so the FULL frame reads "2¹¹ = 2,048", not 2¹²).

## Timeline (clip 15.28 s = 917 frames)
- Frame 0 = x 1 pouring (one ball each mid-fall). Rounds: x1 0.06, x2 0.85, x3 1.63, x4 2.40, x5 3.15, x6 3.89, x7 4.97, x8 6.02, x9 7.38, x10 8.70, x11 9.96 s.
- MOCHI TAKES THE LEAD 1.10 s (4 vs 3, in x = 2). **LEAD CHANGE 9.76 s** (973 vs 974, late in x = 10). **FULL 11.18 s**, then BOLT WINS. Dissolve 14.68-15.28.
- Landings/s: 4 20 53 93 114 186 230 304 433 621 1118 1349 1298 (climbing).

## Sound
- Offenbach, Can-can (Galop infernal, Orphée aux Enfers 1858, PD); notes/harmony = melon_bands' by-eye reading of the 1860 Heugel piano score (`<SOUNDFONTS_DIR>\scores\offenbach_cancan\SOURCE.txt`). 16 bars of 2/4 (strain with 1st ending, strain with 2nd ending), accelerando 150 -> 200 bpm, round lengths 2,2,2,2,2,3,3,4,4,4,4 beats; FULL = the ff D-major downbeat (beat 32).
- Thin -> FULL: strings + violin + pizz (x1-6), + clarinet, horns, basses (x7-9), + brass, flute, tuba, timpani per bar (x10-11), roll + swell into the D-major tutti. Marble clicks per landing group, round ticks, two-ping at both lead changes. Last ~1.2 s silent.

## Checks (encoded Full HD, label b68)
- h264 yuv420p 1080x1920 60 fps, 917 frames = 15.28 s. -14.01 LUFS, peak -4.51 dBFS, last 0.5 s -78 dBFS. flash_check 0 flashes. Seam 0.355.
- Frames read: 0, 1.12 (Mochi leads), 4.0, 9.77 (lead change), 11.19 (FULL: 1,331 vs 2,048, 11³ / 2¹¹), 11.5, 15.2.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch68\growth_race3.mp4`. Owner review: pending.

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/growth_race3.py --still --frame 0,300,700 --label x`
- `NF_SCALE=1.0 python scenes/growth_race3.py --label b68` (~2 min)

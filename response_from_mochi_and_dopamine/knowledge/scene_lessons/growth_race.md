# growth_race — "Mochi adds 100, Bolt DOUBLES" / "whose tank hits FULL first?"

- New franchise, ep. 1 (batch67, research/audience_watch_2026-11-03.md: growth races). New file `scenes/growth_race.py`; no lib/ or tools/ changes.
- Two identical glass tanks, the same FULL line, 1 ball = 1 ball (exact counts). Mochi (coral, left): 0, +100 per round. Bolt (mint, right): 1, x2 per round.
- Counts (end of round): r1 100/2 · r5 500/32 · r9 900/512 · **r10 1,000/1,024** · r11 1,100/**2,048 = FULL**. The brief's numbers were right.

## Layout (side safe zone x 108-907)
- Tanks: Mochi x 118-480, Bolt x 536-898 (0.109-0.831 w). Floor y 1330, FULL y 580 (the top of the 2,048th ball's row), rim y 566. Hoppers y 392-452 labelled "+100" / "x2".
- Balls r 6.0, hex rows of 29/28 filled bottom-up, centre-out. 2,048 balls = 71.4 rows.
- Each round's balls share one hue (same hue in both tanks): Mochi's layers are equal, each of Bolt's is as thick as all his earlier ones together.
- A ball falls straight from the hopper to the pile top, then rolls along the top to its slot (VS 650 px/s).
- HUD: caption (baked, y 150/226), ROUND n (y 336, flips 0.10 s before the round), "ADDS 100"/"DOUBLES" + counts (y 1386/1462, gold = leader), "+100"/"+N" pops under the hoppers.
- Characters sit on the outer rim corners.

## Timeline (seed 2, clip 17.03 s = 1022 frames)
- Round 1 is pre-roll: frame 0 = round 2 pouring (Mochi 100 vs Bolt 2).
- Rounds: r2 0.05, r3 1.61, r4 3.11, r5 4.54, r6 5.91, r7 7.22, r8 8.47, r9 9.66, r10 10.80, r11 11.90 s.
- **LEAD CHANGE 11.76 s** (995 vs 994, late in round 10's pour). **FULL 12.94 s** (beat 44): "FULL!" then "BOLT WINS!".
- Finale: round 12 (Bolt x2 = 2,048 more) drops on the full pile and rolls over both rims (left down the gap, right off-screen); Mochi gets her +100 (1,200). Counter ends 1,200 vs 4,096.
- Dissolve 16.43-17.03 s into the pre-roll.
- Balls landing per second: 67 64 75 71 77 84 110 123 162 230 357 599 1027 1321 (climbing to the finale).

## Sound
- Grieg, "In the Hall of the Mountain King" (Mutopia #1888, Grieg's piano score, PD), beats 4-43 = rounds 2-11, accelerando 150 -> 235 bpm. Statement 1 bassoon + pizz (+12), statement 2 clarinet + pizz + bassoon, the F#-major statement strings + brass + flute; LH ostinato on pizz/contrabass/tuba; timpani on every half bar from beat 20, a roll into beat 44.
- Beat 44 = B-minor tutti (choir, strings, brass, timpani, boom, crash) = FULL.
- Held phrase-end notes at 0.6 velocity (the bassoon's held A at 5.3 s was +6 dB over the body before).
- SFX: marble click per landing group (>= 12 ms apart, density-ducked), rim/fall clicks for the spill, a soft tick per round, a two-ping at the lead change. Last ~1.2 s silent.

## Checks (encoded Full HD `output/growth_race_b67_9x16.mp4`)
- h264 yuv420p 1080x1920 60 fps, 1022 frames = 17.03 s.
- -14.01 LUFS, peak -5.07 dBFS, last 0.5 s -74.7 dBFS. RMS/s -17.1 -17.5 -17.2 -16.8 -16.3 -14.8 -16.6 -17.6 -16.9 -16.7 -17.0 -18.1 -16.4 **-13.0 -13.7** (FULL) -21.1.
- flash_check 0 flashes. Seam 1.08 (interior steps 1.03-1.08 at Fast; the stream is always moving).
- Frames read: 0, 0.5, 2, 5, 9, 11.0, 11.8 (lead change), 13.1, 13.3, 16.0.

## Doubts
- Bolt's tank is almost empty for ~7 s (2-64 balls): the honest exponential.
- The lead change is a photo finish (995 vs 994 when it flips; 1,024 vs 1,000 at the end of the round).
- Mountain King is used a lot on this channel (and in the atom long video).
- Rounds 10 and 11 hues (blue-violet / purple) are close.

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/growth_race.py --still --frame 0,400,708 --label x`
- `NF_SCALE=1.0 python scenes/growth_race.py --label b67` (~2 min)

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch67\growth_race.mp4`. Owner review: pending.

## Music swap (2026-11-03, `--music hd5`; default `mk` stays bit-identical, verified max diff 0)
- Why: Mountain King is overused (atom long video). Brahms, Hungarian Dance No. 5 (pub. 1869, PD), melody from the flutetunes MIDI as sand_rise4 (`brahms_hungarian5_dl`); harmony = sand_rise4's oom-pah chord table.
- Grid beat g = score quarter g + 18: rounds 2-11 = score beats 22-61 (end of phrase 2 + its 16th run, the full 3rd statement, the high 4th statement and its 16th run), FULL (beat 44) = score beat 62, an F#-minor tutti. Same accelerando 150 -> 235 bpm.
- Orchestration: clarinet + violin (s1), violin + strings + clarinet + bassoon (s2), strings + brass + clarinet + flute + horn/choir pads + tuba (s3); pizz oom-pah throughout, contrabass octave bass, timpani per bar from beat 20, a roll into beat 44.
- Audio-only: `ffmpeg -i review/growth_race.mp4 -an -c:v copy output/growth_race_hd5_9x16_silent.mp4`, then `NF_SCALE=1.0 python scenes/growth_race.py --music hd5 --reuse --label hd5`. Video stream md5 identical to the MK file.
- Checks: -14.01 LUFS, peak -5.43, last 0.5 s -78 dBFS; RMS/s -18.7 -18.2 -17.2 -16.9 -18.2 -18.6 -19.0 -17.9 -16.8 -17.3 -15.9 -15.2 -14.5 **-13.8 -14.3** (FULL) -22.7; 78 melody notes, 17 distinct; 137/140 spectral-flux onsets within 40 ms of an event (MK file 160/166).
- Lost: Bolt's first 14 balls (rounds 2-4) were placed on MK's onsets; with HD5 they are not on melody notes (their own clicks remain).
- Delivered as `review\batch67\growth_race.mp4`; the MK file is `growth_race_mk.mp4`.

## 4K (batch68, owner OK on the Mountain King version)
- `NF_SCALE=2.0 python scenes/growth_race.py --label b68_4k` (default `--music mk`): h264 yuv420p 2160x3840 60 fps, 1022 frames = 17.03 s, −14.01 LUFS, peak −5.07 dBFS, last 0.5 s −74.7 dBFS, flash_check 0. Frames 11.8 / 13.1 s read. Not staged: `<VIDEOS_DIR>\MochiAndBolt\review\batch68\growth_race_mk_4k.mp4`.

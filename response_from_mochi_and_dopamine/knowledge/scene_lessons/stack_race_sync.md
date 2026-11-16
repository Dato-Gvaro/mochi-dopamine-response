# stack_race_sync

- Owner review of stack_race s498 (2026-10-04): "the async sounds don't make it satisfying ... for a couple of seconds let both hit IDENTICALLY, three or five jumps". This file is stack_race plus SYNC STREAKS; stack_race.py stays reproducible. It reuses stack_race's sim, draw and reactions and replaces race().
- Sync streak: once both lanes' next slide starts at or after the plan time, N drops are forced PERFECT on the SAME frame. The landing time is T = the later lane's ready time + AMP/v, snapped to mid-frame. Each lane's slide starts at T - AMP/v (its own speed). Sliders come in mirrored (both from the outside, then both from the inside). The pause between drops is a fixed 0.10 s. Outside the streaks the lanes alternate naturally (seeded re-aim pause).
- SYNC_PLAN = [(14.0, 3), (29.0, 5)]: a short streak mid-race and a 5-hit streak about 4 s before the miss.
- Sound: a synced pair is ONE hit, centred: melody note + its 5th at +12 ms + octave and small pop at +24 ms. The +12 ms offsets get past the mixer's 10 ms onset rule. Everything else is as in stack_race.
- Visual: a small yellow "SYNC!" pops on the divider at each synced hit (0.5 s), next to both "Perfect!" stamps. No "worried" faces within 0.6 s of a synced hit.
- Seed 498 no longer ends with Bolt winning under any plan (14-17 s / 22-29 s), so the seed changed. The search wanted a Bolt win, the 5-hit streak ending 1.8-4 s before the miss, and a close finish.
- s1252 (default): Bolt wins 84 vs 84 levels. Mochi misses at 34.12 s on a 24 px top (Bolt's top is 40 px). Syncs at 14.76, 15.19, 15.62 and 29.34, 29.59, 29.84, 30.07, 30.31 s. Clip 38.22 s. Drops/5 s: 15, 19, 24, 30, 35, 45. Distinct hits/5 s: 15, 19, 21, 30, 35, 40. Height lead changed 8 times, width lead 12.
- Args: --seed (1252), --label, --cap, --melody, --search N, --still --frame.
- 4K ship render (`--label ship`, NF_SCALE 2.0): h264 yuv420p 2160x3840, 60 fps, 2293 frames. -14.00 LUFS, peak -7.45 dBFS, last 0.5 s -72.2 dBFS. Seam mean 0.143. flash_check: 3 flashes, worst 1 per s = PASS. Pre-encode seam max 27/255 on 17 px. Synced chords checked in the events file (e.g. 29.342 / 29.354 / 29.366 = 64 / 71 / 76).
- Shipped 2026-10-04 to Schedule/2026-10-05/stack_race.mp4, replacing the s498 non-sync cut.
- Owner review 2026-10-05: Pulled: try one stacking while the other interrupts -> stack_sabotage.

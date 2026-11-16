# comment_overflow2 — "Every ball CRUSHED splits in 2" / "until a 64-bit counter breaks"

- Sequel to comment_overflow (11.4K), batch67. New file `scenes/comment_overflow2.py` (a copy of comment_overflow v6); ep. 1 untouched, no lib/ or tools/ changes.
- **ONE nameable change: the 64-bit counter.** 63 doublings to 2^63; the counter shows 9,223,372,036,854,775,807 (INT_MAX, ep. 1's convention), "+1", glitch, then -9,223,372,036,854,775,808 (`int64()` wrap) and the collapse.
- Kept from ep. 1: the granular sim, x2 press, containers that break and zoom out to a bigger one, "ball = M balls" legend from wave 11, glitch, red negative, collapse on the cadence, Mochi wow -> annoyed, Bolt laughs, music-first leveller and post-master fade.

## Changes vs ep. 1
- **No comment card** (nobody asked for 64-bit; none invented). `CARD_HOLD`/`CAP_IN` = -9, so the caption is up from frame 0.
- 10 containers: 8 + 6 x 8 + 7 = 63 waves (`JARS`, `_plan()`). Hue drift 36 deg per jar.
- **Honest container labels:** what 2^n 1 cm marbles (~0.82 mL each packed) fill at each container's last wave: CUP 0.3 L (256 -> 0.2 L), BUCKET 15 L (13 L), HOT TUB 1,000 L (860 L), TANKER TRUCK 60,000 L (55,000 L), WATER TOWER 4 million L (3.5M), SUPERTANKER 300 million L (225M), RESERVOIR 15 billion L (14B), LAKE 1 trillion L (0.9T), LAKE GENEVA 89 trillion L (59T), LAKE SUPERIOR 12 quadrillion L (7.6 quadrillion = ~63 %). Name + capacity on the housing; footnote "sizes: if every ball were a 1 cm marble" under the goal.
- Goal line "/ 9,223,372,036,854,775,808" at 40 px, max 540 px (between the characters).
- Milestones up to 1 QUINTILLION (10^3 ... 10^18).
- Simulation cap 45 s (was 30).

## Music
- Bach, WTC I Prelude in C minor BWV 847 (Mutopia #550, PD), bars 1-16 both hands as written, one steady tempo Q = 0.44 s (136 bpm). Piano + a soft strings/contrabass pedal on each half-bar's lowest note (no chord pad: the figure's neighbour notes would make clusters), crescendo 0.46 -> 0.68.
- Flip on beat 64 = our rolled C-minor chord (piano, strings, contrabass, oohs) after bar 16's dominant. Tinkles/blips re-keyed to C minor.
- Plan (beats): jar 1 contacts 0.5-4.0, break 5.5; then break -> +1.5 -> 6 contacts at spacing 1.0, 1.0, 0.75, 0.75, 0.6, 0.6, 0.5, 0.5 -> break +1.5 (last +1.0); jar 10: 7 contacts 59.0-62.0; +1 at 63, flip at 64.

## Timeline (seed 0, clip 30.68 s = 1841 frames)
- Breaks 2.43 / 5.95 / 9.47 / 12.43 / 15.40 / 18.05 / 20.68 / 23.10 / 25.30 s.
- Milestones: thousand 3.67, million 8.93, billion 14.17, trillion 19.05, quadrillion 22.50, quintillion 26.68 s.
- 9,223,372,036,854,775,807 at 27.37 s, +1 27.72 s, flip 28.17 s, end 30.67 s.
- Press strokes per 5 s: 14, 6, 12, 12, 14, then 7 in the last 2.3 s (the opening jar's 8 quick waves front-load the count).

## Checks (encoded Full HD `output/comment_overflow2_b67_9x16.mp4`)
- h264 yuv420p 1080x1920 60 fps, 1841 frames = 30.68 s.
- -14.01 LUFS, peak -5.51 dBFS, last 0.5 s digital silence. RMS/s flat -16.3...-16.9 (leveller), flip second -13.9 (+2.6 dB).
- flash_check 0 flashes. Seam 0.97 (ep. 1: 0.94).
- Notes 256 (RH), 17 distinct, top 18.8 %.
- Frames read: 0, 3.0, 14.17, 21.0, 27.45, 28.3, 29.5, 30.6.

## Doubts
- 30.7 s vs ep. 1's 19.8 s (twice the doublings). The first ~10 s are no faster than ep. 1.
- No comment card = ep. 1's hook is gone; frame 0 is one ball in a cup.
- The steady 16th-note Bach is busy under a busy picture.

## Commands
- `NF_FAST=1 NF_SCALE=1.0 python scenes/comment_overflow2.py --cache --still --frame 0,150,1650`
- `NF_SCALE=1.0 python scenes/comment_overflow2.py --cache --label b67` (~3 min)

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch67\comment_overflow2.mp4`. Owner review: pending.

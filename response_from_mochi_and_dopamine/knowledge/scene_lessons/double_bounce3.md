# double_bounce3: fast-finish cut of double_bounce2 (Circle vs Square, every bounce DOUBLES the ball)

## Owner review it answers

Owner review of double_bounce2 (2026-10-15): "after ~15 s make it quick, the wait for the burst is too long, progress is not visible, boring; remove the ball tails".

## What changed

- **No trails:** plain glowing balls from frame 0.
- **HEAT law (time-based, the same for both arenas):**
  - From 13 s every ball's speed is multiplied by 1 + 0.06 (t - 13)^2.
  - The count-based laws are unchanged: speed 520 -> 9 px/s with a knee at 2^6, radius 80 -> 0.2 px.
  - A count-based speed-UP was tried first and rejected: the leader runs away (×10 margins), so there is no close race.
- **Visible progress, every second:**
  - PRESSURE bar per arena (log2 count / 20) at y 1300.
  - The arena's inner glow heats up.
  - The wall goes neon -> white, trembles, and bulges up to 12 px (visual only).
  - 9 white-hot cracks grow past 45 % stress.
  - The counters pop at 10, 100, 1k, 10k, 100k, 250k, 500k, 750k and 1M.
- **Photo finish:** the runner-up bursts too (second shard spray and a second glass crash). The winner's counter alone turns gold.
- **Kept from double_bounce2:**
  - Mid-action frame 0.
  - Palette: coral/gold circle, teal/mint square.
  - Faces at r 52.
  - Rondo alla Turca (K.331, PD) on marimba, one octave down.
  - Burst at real speed, then the dissolve loop.
  - Hold 1.4 s after the first burst, then a 0.7 s dissolve.
- **Watermark** moved to y 1590.

## Race (seed 12 of double_bounce2 does not carry over)

Searched 26 seeds.

- **Seed 13:**
  - Counts, circle/square: 2 s 16/19, 5 s 466/486, 10 s 8,723/9,768, 15 s 48,247/57,536, 18 s 156,485/181,427.
  - The square leads from 2 s. The CIRCLE takes the lead at 20.3 s and bursts at 21.50 s (the square on 901,997).
  - The square bursts 0.32 s later.
- **Search criterion:** the runner-up must burst within ~0.35 s, so its crash still lands before the silent tail.

## Checks (encoded Full HD v1)

- **Format:** h264 yuv420p 1080x1920 60 fps, 1416 frames = 23.60 s.
- **Loudness:** -14.01 LUFS, peak -5.6 dBFS.
- **Tail:** last 1.3 s at -105 dB. The audio fade runs from the second burst +0.25..0.48 s.
- **Loop seam:** 0.334.
- **flash_check:** 0 flashes, PASS, mean luminance 0.045.
- **Notes:** 25 distinct, top note 14.9 %. Sound events per 5 s: 94, 168, 217, then 191 in the last 3.6 s (rate still climbing).
- **First sound:** at 0.1-0.35 s, with digital silence before it.
- **Frames read:** encoded frames at 0, 1, 2, 15, 18, 20.5, 20.8 (crop: cracks and bulge), 21.55 and 21.9 s.

## Delivery

- Delivered <VIDEOS_DIR>\batch33\double_bounce3.mp4. Owner review: pending.

Owner review (2026-10-15): approved ("it's ok") -> 4K Schedule/2026-10-18 slot 1.

- Owner review (2026-10-15): approved ("it is ok"). 4K ship render (NF_SCALE=2.0, --label ship, seed 13): 2160x3840 h264 yuv420p 60 fps, 1416 frames = 23.600 s, -14.01 LUFS, peak -5.6 dBFS, seam 0.226, flash_check PASS. Staged <VIDEOS_DIR>/Schedule/2026-10-18/1_double_bounce3.mp4 (516 MB).

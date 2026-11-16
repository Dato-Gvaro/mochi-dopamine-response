# island_ch3b_coconut (STRANDED ch3b COCONUT): 9:16 Short notes

General chapter notes: docs/scenes/island_long.md.

## 9:16 4K fix (owner review 2026-11-08: "picture jumps like skips or fast-forward")
- Jumps found: 4 hard time cuts in the 9:16 EDL at 4.6 / 8.2 / 10.2 / 12.8 s (clock skipped 6.0 / 1.2 / 3.71 / 1.39 s), plus a layout pop at 16.92 s (the meters vanished in one frame at C_WHY).
- Fix (9:16 only, every change guarded by orientation; the 16:9 is bit-identical, frames + audio build tested):
  - `lib.island.RampEdit`: each cut is a C1 speed ramp through the skipped clock, v = 1 + (2G/W) sin^2(pi s/W).
    - Windows (hb, ha) = (0.5, 0.9), (0.5, 0.5), (0.4, 0.6), (0.4, 0.4) s.
    - Peaks x38 / x85 / x8 / x45 real time (tug x4, settle x25, throws x10 included).
  - `ramp_frame`: real shutter motion blur (K sub-frames averaged); outside the ramps the frames are exact.
  - A "▶▶ xN" tag shows the ramp's honest peak, at (108, 470).
  - The 9:16 caption "Bolt waits for it to settle." now spans the ramp (c 13.75-15.75). "(x25)" was dropped: the tag carries the factor.
  - The meters fade out over 0.35 s before C_WHY.
- Length unchanged: 18.32 s / 1099 f. The sound was rebuilt from events because the marks inside the ramps moved. Throws #3-#7 are now heard and seen.
- Scene-score max at the old cuts: 0.007 (was 0.031-0.041).

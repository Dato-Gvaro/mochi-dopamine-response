# lava_ice2 — faster, shorter lava_ice (owner 2026-10-13: "good but too long and slow")

Same rules as lava_ice (docs/scenes/lava_ice.md). Changes, per research/scroll_stop.md:
- Board 44x44 in the circle (1,468 cells, cell 21.5 px vs 15.8): reads at thumbnail size.
- SUB = 2 sim ticks per frame (twice the pace); gscale 85 (smaller board = shorter chains).
- Frame 0 = 0.8 s before first contact (`playback()` cuts the warm-up): both blobs already
  growing on a collision course (LAVA 10 vs ICE 9), contact and first lead flip by 0.5 s.
- Faces bigger (r 42), lead banner moved above the arena (y 372) so it never covers them.
- Finale 1.5 s sweep + "ICE TAKES THE WHOLE BOARD!", then a 0.7 s DISSOLVE to the frame-0
  board (counters swap at the midpoint, gaze glides back) instead of a rewind.
- Sound denser: pop gap 0.05 s, crackle gap 0.035 s, melody gap 0.30 -> 0.16 s (Habanera,
  marimba); tune walks on growth for the first 1 s, then on walls/breakthroughs.

## Seed 209 (search: race 17-26 s, >= 3 debounced flips, smallest max gap between flips)
- Lead: ICE 0.5 s · LAVA 1.7 s · ICE 2.7 s · LAVA 7.4 s · ICE 13.8 s · full board 18.27 s.
- Counts: 4 s 362/410 · 8 s 735/659 · 12 s 859/514 · 14 s 667/686 · 16 s 246/1157.
- Clip 20.47 s (race 18.27 + 1.5 + 0.7).

## Checks (Full HD, <VIDEOS_DIR>\batch31b\lava_ice2.mp4)
- h264 yuv420p 1080x1920 60 fps, 1228 f. LUFS -14.01, peak -7.5 dBFS, last 0.5 s -56 dB.
- flash_check ok (1 flash, the finale sweep). Seam post-encode mean 0.63 (good band).
- Notes 89, 13 distinct, top 17 %; melody notes/5 s 20-21-26-22.
- Encoded frames 0/0.5/1/2/3/7.5/14/17/18.8/20.3 s read correctly.
- Gap between flips 7.4 -> 13.8 s (6.4 s) is the longest stretch without a lead change.
- Owner review (2026-10-15): ok, this will do -> APPROVED, 4K (Oct 17 slot 2).

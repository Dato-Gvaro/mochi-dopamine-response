# ol_sand_vs_stars2 (DopamineEXE, owner review docs/REVIEW_1114.md)
- v2 of `ol_sand_vs_stars` (v1 untouched). Owner 2026-11-14: OK, show the numbers more visibly, ON the jars, riding the fill level.
- ONE change: `draw_jar_label()`. Each tube carries a dark pill (214 x 96 px, the side's colour rim) with the count: number 56 px white + black outline, word 25 px in the side colour.
  - The pill's top edge sits on the fill surface (`ly(level)`), so it rides up as the tube fills; clamped inside the tube (at the bottom for 1 / teaspoon / 9,100).
  - Same value as the header counter (`fmt_count(level())`), eased with the fill; pops 1.18x on each rung of that side.
  - x 193-822 (the pill overhangs the 150 px tube by 32 px a side): inside the 0.10-0.84w side-safe zone; the axis words at x 422-592 stay clear.
- Everything else is v1: rungs, facts, header counters, status pill, the to-scale finale, music, length 15.27 s.
- FHD verified 2026-11-14: 15.27 s, -14.0 LUFS, peak -5.6 dBFS, flash PASS (0), seam 0.26. Review: `<VIDEOS_DIR>\DopamineExe
eview\ol_sand_vs_stars2.mp4`.

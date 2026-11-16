# stack_sabotage2: 20 glowing levels in 15 s, 7 unique gags

- Owner review of stack_sabotage (2026-10-05): "better but too large, make it SHORTER; instead of repeating the interruptions make each one UNIQUE". v1 is untouched.
- Look: the ring_escape2 dark jewel stage. Navy -> plum gradient with parallax specks, a smoked-glass lane and a colour pool behind the tower top. Blocks are glowing jewel glass (layered glow, gradient core, top sheen), ruby -> orchid by level. The top block glows brighter for 0.35 s when it lands. Gold goal line "GOAL 20". The timer bar has a jewel glow (teal -> ruby).
- Rule: same stacking core (slide, drop, slice, a perfect = octave + ring + "Perfect!", 2 perfects regrow +20). Goal: 20 levels before the 15 s timer runs out. Caption "Mochi stacks, Bolt sabotages|~20 levels in 15 s~". W0 420, BH 62, TX 610. Speed 420 + 700*((k-1)/19)^1.1 px/s. First drop at 0.47 s.
- Readable top: a slice never leaves the top narrower than WMIN 170 (the extra overhang stays as a ledge). A drop more than 34% off its base TIPS OFF (MISS, the level is retried).
- 7 gags, each used ONCE, escalating, each with its own physics and its own sound. Mochi aims at only 30% of the sway.

| # | Gag | t (s) | Effect | Sound |
|---|---|---|---|---|
| 1 | Paper plane | 2.18 | taps the slider +24 px | pok flick + tap |
| 2 | Slingshot pebble | 2.95 | 9 Hz shiver | band snap + clank ping |
| 3 | Fan | 4.92 | gust +40 px on the slider | servo spin-up + puff |
| 4 | Magnet | 7.28 | drags the slider -55 px | zap + latch clack |
| 5 | Lasso | 8.50 | yank, sway -58 | rope ratchet creaks + whip snap |
| 6 | Bowling ball | 10.40 | rolls down a plank into the side: sway +72 + shiver | roll ticks + slam |
| 7 | Wrecking ball | 12.45 | swings off the crane into the top: sway +125 + shiver | chain ticks + big slam |

- Reactions: Mochi gets one per gag (wow, wince, worried, annoyed glare at Bolt, worried, wow, worried) and cheers twice at the win. Bolt does a mischief tell before each gag, laughs at gag-made slices >= 28 px or a miss (4x), and stares annoyed at the camera at the end.
- Sound: eine_kleine note per placed block. Notes are spaced >= 12 ms first, then foley is nudged +12 ms off them. Silent tail.
- Loop: the tower sinks into the plinth, the colour pool fades back to level 1, the timer refills, Mochi returns to her frame-0 mid-hop pose, and the slider ghosts back in. Fully sunk blocks are skipped, because their glow leaked over the plinth at the seam. Pre-encode seam max 3/255 on 1 px.
- Search `--search N`: keeps wins with 0.15-0.8 s spare and all 7 gags. Score = misses, big slices, drama after the wrecking ball, minus spare time.
- s200 (default):
  - The wrecking ball makes level 17 TIP OFF at 12.61 s. The retry slices 26 px. Mochi lands level 20 at 14.76 s with 0.24 s to spare. Final top: 170 px.
  - 21 attempts. Drops/5 s: 8, 12, then 5 in the last 4.76 s, i.e. ~13 per 5 s. Clip 18.57 s.
- Checks (encoded Full HD): h264 yuv420p 1080x1920, 60 fps, 1114 frames. -14.00 LUFS, peak -7.30 dBFS, last 1.3 s at -90 dBFS. Seam mean 0.199. flash_check: 0 flashes = PASS (mean lum 0.033).
- Args: --seed (200), --label, --cap, --melody, --search N, --still --frame.
- Delivered <VIDEOS_DIR>\batch14\stack_sabotage2.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-06: Good; could be more STRESSFUL.

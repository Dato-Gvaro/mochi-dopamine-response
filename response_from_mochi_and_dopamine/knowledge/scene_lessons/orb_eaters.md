# orb_eaters — Mochi and Bolt EAT glowing orbs, Line by line vs Freestyle (new scene; vacuum_strategy stays reproducible)

- Why: owner review of vacuum_strategy: "better, but what if they EAT them? The vacuum tubes look like snakes." The owner chose glowing energy orbs (not candy: made-for-kids risk).
- Rule: each half of a dark tiled floor holds the same 120 orbs (mirrored layout). The first to eat ALL its orbs wins. Caption "Line by line vs Freestyle|~First to eat ALL orbs WINS~", in the same left/right order as the characters.
- No hoses or tanks. The floor is taller (y 352..1300).
- Eating: an orb inside the eater's aura swirls into its open mouth (1.7 rad swirl, 3 motion ghosts, stretch). Pull-in time is 0.16 + 0.0016*d, so a cluster streams in near-first.
- Mouth: it opens wider while orbs are in flight (0.35 -> 0.95) and chomps (closes plus a squash) for 0.12 s on each arrival. Each orb ends with a glow pop: a ring in the orb's colour and 4 white sparks.
- The eater grows +26% radius over 120 orbs, and its body glow rises 0.15 -> 0.75.
- Orbs: soft halo, white-hot core and highlight. 6 neon colours on a dark floor (0.13, 0.12, 0.22).
- Coverage: a floor tile lights up in the eater's colour when its aura passes (mixed 32% toward the body colour), with a glint. Each path stays as a faint light trail: Mochi's lanes read as stripes, Bolt's freestyle as a scribble.
- Strategies: `--free 1` (the default) makes BOLT freestyle and MOCHI line by line. Mochi wins via the comeback, as the coordinator suggested; it is the vacuum_strategy story with the roles swapped.
  - Freestyle and lanes are the same as vacuum_strategy (greedy n^0.5/(d+40), rho 85, 9 lanes, g 1.12..1.18).
- Late-rate dip FIXED: COVER is 0.60 (it was 0.42), so each lane's aura only slightly overlaps the next lane and the top lane keeps its own orbs. Tail (rate in the last 1 s / the 3 s before) is 1.2 for s201; vacuum_strategy's pick was 0.64.
  - Side effect: lanes beat freestyle in ~97% of seeds.
- Layout: start clusters at the start corners are big (START_W 1.4), so both eat 5-8 orbs by 0.5 s. Clusters are biased to the top. The end strip runs along the top wall by the divider.
- Finish: "MOCHI WINS!" is 156 px (max width 960) at y 840. The winner's aura swells across the divider and eats the loser's leftovers, but only if the radius stays <= 340. Otherwise the steal is skipped and the leftovers stay on the floor.
- Loop: the eaten orbs pop back onto their spots top-first (over 0.8 s), counters and body size fall with them, tiles go dark top-down, trails fade, and the eaters glide home.
- Seed s201 (search 2500): Mochi 38:36 at 8.5 s. Bolt leads 57:47 at 10.5 s; it is 110:110 at 14.6 s. Mochi takes the lead at 14.7 s and wins 120:117 (Bolt needed ~0.1 s more). Final 123:117 after the steal (R_big 335). Lead changes are m 8.1, b 10.0 and m 14.7 s, with the largest gap 36.
  - Captures per 3 bins: [47, 49, 141].
  - Alternates: s846 (Bolt up 93:47 at 10 s, cleaner escalation, tail 2.07); s212.
- Measured (Full HD encode): 19.50 s, 1170 frames, h264 yuv420p 1080x1920 60 fps. -14.0 LUFS, peak -7.3 dBFS, last 0.5 s -80.8 dBFS. flash_check PASS (0 flashes). Pre-encode seam max delta 0; post-encode mean 0.61.
- Sound and rate: sounded notes per 2.5 s are 19, 11, 14, 17, 33, 35, 13. 142 notes, 25 distinct, top pitch 11%.
- Doubts:
  - The rate dips at 2.5-5 s after the opening burst, then climbs to the end.
  - In-flight orbs pass over the eater's face for a moment before they reach the mouth.
- Args: --seed (201), --free (1), --label, --cap, --melody, --search N [--from S] [--want 0|1], --dry, --still --frame.
- Delivered <VIDEOS_DIR>\batch13\orb_eaters.mp4. Owner review: pending.
- Owner review 2026-10-05 night: GOOD. Frame the title/caption around 'which strategy is better'.
- Owner review 2026-10-05: GOOD. "Frame it like 'which strategy is better'."

## orb_eaters2 (strategy framing; scenes/orb_eaters2.py, a thin wrapper)
- Same seed (201), race, sound and loop as orb_eaters. The wrapper turns on two options in orb_eaters.py; both are off by default, and the default orb_eaters frame is pixel-identical after the edit.
  - `STRAT_LABELS`: "LINE BY LINE" / "FREESTYLE" (46 px, in the characters' colours) at y 1368 under each half; the counters move to y 1458.
  - `END_LINE`: "LINE BY LINE wins" (78 px, the winner's colour) pops in 0.2 s after the banner, at y 970.
- Caption "Which strategy is BETTER?|~First to eat ALL orbs WINS~". Line 1 asks the question the video answers; line 2 is the rule (not a viewer-prediction question).
- Measured (Full HD encode): 19.50 s, 1170 frames, h264 yuv420p 1080x1920 60 fps. -14.0 LUFS, peak -7.3 dBFS, last 0.5 s -80.8 dBFS. flash_check PASS (0 flashes). Pre-encode seam max delta 0; post-encode mean 0.64.
- Delivered <VIDEOS_DIR>\batch14\orb_eaters2.mp4. Owner review: pending.

# bean_push2: RAKE vs LEAF BLOWER (sequel to bean_push, 2026-11-14)

- Review: `<VIDEOS_DIR>\MochiAndBolt\review\bean_push2.mp4` (+ `_files\README.md` with the 3 ideas and the pick). New file; bean_push.py untouched.
- The ONE change: autumn LEAVES, a rake (Mochi) vs a leaf blower (Bolt). Same pile → bag race, the same 1.5x-bigger-every-pass rule, the same engine and Carmen.
- Rake = bean_push's blade, physically (same seed and pile → the same FULL at 13.33 s). The leaves are discs drawn as leaves (`draw_balls`: a pointed oval + midrib, turning with travel).
- Blower = `Balls.jet()`: a cone ahead of the nozzle (half-width w/2 + 0.22·s, reach L_J 320, push falls linearly). 28 rays; rank-k leaf in a ray gets exp(−k/2.5) (shielding). 35% of the push is sideways (fan-out). A_J 6000 → a lone leaf reaches 6000/7 ≈ 860 px/s ≈ 2x the rake's 420 (chosen on that principle, not tuned for the result). It never collides or stalls; it stops 90 px short of the bag line.
- Jetted leaves are exempt from the REST_V zeroing (otherwise they creep at the per-substep Δv: 25 px/s < 30).
- Seed 1: bag % rake/blower: 2 s 8/5, 4 s 8/13, 7 s 14/32, 9 s 38/54, 11 s 71/56, 13 s 83/70; leads: blower at 8.65 s, rake at 10.38 s; rake FULL at 13.33 s (blower 82%). Clip 15.93 s.

## Rejected sequel ideas (tested in sim, files in output/tmp/builderM/)
- SNOWPLOW (V) vs flat blade on a road with the snow doubling per section: in 2D the flat blade spills off its ends exactly like the V casts aside. Both finished within 0.5 s (blade ahead), and nothing stalled even with snow-like friction (μ 0.8, roll 40). The V's real edge (throwing snow UP onto banks) is 3D. Making it win would have meant faking it.
- UPHILL bean_push (G_HILL 700-1500, valley pile): the cup led, then the wider blade won at every setting. It's the same story as bean_push. Also: a bag on a slope needs G_BIN ≥ 2400 or it leaks back out.

## Outcome
- (fill after review)

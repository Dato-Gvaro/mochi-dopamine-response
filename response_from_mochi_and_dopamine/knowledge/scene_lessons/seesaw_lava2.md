# seesaw_lava2
- Owner on seesaw_lava (2026-10-05): "very good, I like these colours" but the grey peg triangle/dispenser don't match the cave; change the ball colours. New file; seesaw_lava.py stays reproducible (s201 re-simulated identical after a whitespace-only cleanup of doubled blank lines in its header).
- Same physics/rule/dunk/smoke/soot/loop/sound as seesaw_lava. Look only: hanging basalt vent with a glowing crater mouth (flares on each drop); cracked basalt rock face behind the pegs with glowing seams; ember-stud pegs (dark stone, glowing core that swells/brightens on hit); stone funnel walls with a glowing seam; stone wedge; stone fulcrum; iron pivot; iron cage baskets (team-colour stripe on the rim); ember-spark confetti.
- Balls = MAGMA ROCKS: glowing ember gradient (red/orange/gold/amber) with dark crust cracks; 1 tint in 7 = obsidian pebble with an orange seam. First try (dark rock + glowing cracks) was unreadable on the dark baskets/rock face.
- Dunk point moved to the board end +8 px (was +34) so Bolt's dunk stays out of the right-edge UI strip.
- Search bonus now favours a Bolt loss (Mochi wins; Bolt won seesaw2 + seesaw_lava).
- s401: Bolt in the lava at 23.37 s, Mochi wins 35-42. 72 balls, 8 lead changes; Mochi was 3 down at ~19 s, then Bolt went 0 -> +8 in the last ~15 landings. Landings/5 s: 13, 16, 20, 23. 28.67 s.
- Checks: h264 yuv420p 1080x1920 60 fps; -14.0 LUFS, peak -7.1 dBFS; last 1.3 s peak -70.6 dBFS, last 0.5 s silent; flash_check PASS (0); seam mean 0.402.
- Args: --seed (401), --label, --cap, --melody, --search, --still --frame.

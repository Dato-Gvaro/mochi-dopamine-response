# bubble_battle — Mochi vs Bolt, two trampolines

- Episode of bolt_bubbles3. Nameable change: HEAD-TO-HEAD — Mochi (left) and Bolt (right) each on a trampoline under the same two machines; a pop counts for whoever reaches the bubble first. Counters "MOCHI N vs BOLT N" at 0.775h; a crown rides on the leader (0.4 s hysteresis, pops in on a lead change); the leader's counter turns yellow.
- Rule unchanged (bb3 bubble model + aiming + air control, imported from bolt_bubbles.py). Rate 4.4 + 12.6*u^1.2 /s (bb3: 3.6 + 10.4) for two players, big share 0.25 -> 0.65.
- Personalities: Mochi r 92, g 1450, air control 1250, vy0 -1150..-1350 (1.6-1.9 s floaty jumps, combos to x38); Bolt r 78, g 2700, air control 2900, vy0 -1050..-1350, 0.08 s contact (quick hops, ~2x the jumps). Balance knob = size: at r 84/84 Bolt won 299/300 seeds by ~66; at 92/78 mean diff -13, sd 20, ~3.5 lead changes.
- Each player is clamped to its half (Mochi x <= 446, Bolt x >= 634) and only targets bubbles over its half. Pop sparkle = droplets in the popper's colour + a star flash.
- "xN!" combo only from 20 (12 put ~20 labels on screen).
- End (tau after the machines stop at 26 s): last jumps land home by 1.0; 1.15 result — crown snaps to the winner, "WINNER!" sticker, winner cheers twice, 3-note fanfare 72-76-79; the loser glances at the winner, then watches a stray small bubble drift from its own machine; 1.95 it pops on the loser's head (wince 0.28 s, pop + pok, no tonal note), then annoyed stare at the camera; last 0.45 s everything eases to frame 0 (bb3's loop: leftovers fade, frame 0's own bubbles rise into place, counters roll to 0, highlight fades). Pre-encode last frame == frame 0 (max delta 0).
- Seed search (`--search N`): seed 60 = 273-271 Mochi, 8 lead changes (2.9, 3.9, 8.8, 13.1, 14.7, 20.6, 22.1, 25.05 s). Other close seeds: 3 (283-279 Mochi, overtakes on the very last jump), 71 (274-275 Bolt), 198 (287-287 tie — unusable).
- Sound: PD "mountain_king" walker shared by both (pops +12, small +24, panned by x), bounces per landing (Mochi's bigger), foley nudged +12 ms off any onset < 11 ms. Nothing in the last 1.3 s.
- Args: --seed (60), --dur (26), --label, --cap, --sim, --search N, --still --frame.
- Measured (encoded, s60): 29.42 s (1765 frames), h264 yuv420p 1080x1920 60 fps, -14.0 LUFS, peak -4.8 dBFS, last 0.5 s -62.4 dBFS, flash_check 0 PASS, post-encode seam mean 0.34. Pops per 5 s (main 26 s) Mochi [26, 22, 49, 70, 102], Bolt [20, 29, 47, 70, 100]; sound events/5 s [43, 48, 68, 86, ...] (pop gate 0.04 s).
- Known nit: crown hysteresis 0.4 s means the crown/yellow counter can sit on the player that is 1 behind for a moment (e.g. 0.5 s: MOCHI 2 crowned vs BOLT 3).
- Delivered <VIDEOS_DIR>\batch7\bubble_battle.mp4. Awaiting owner review.
- Owner review 2026-10-04 (batch 7): OK, as long as it isn't too similar to bolt_bubbles3 or reads as lazy -> schedule >=3 days after it.
- Owner review 2026-10-04: Same made-for-kids worry (soap bubbles) -> orb_battle (glass orbs). Pulled from Oct 9.

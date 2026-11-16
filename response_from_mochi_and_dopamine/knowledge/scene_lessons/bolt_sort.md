# bolt_sort
- Rule: candies drop from a dispenser; Bolt slides on a plank and head-bumps each into the jar of its colour. Every candy goes in its jar.
- Escalation: drop rate 1.4/s -> ~5.7/s (`--spawn 31` = seconds to drop all 100). Bumps per 5 s: 8, 11, 15, 19, 25.
- 4 jars x 25 (7-row hex stack); colour order shuffled in blocks of 8 so all 4 jars go FULL in the last ~0.5 s (31.6-32.1 s).
- Analytic sim (closed-form fall -> bump arc -> slot); Bolt's path is planned between catches (peak ~1670 px/s).
- Loop: confetti, then jars hop, flip, pour out and flip back; Bolt glides home -> frame 0 (RESET 2.0 s).
- Sound: bump = korobeiniki note + bounce; jar landing = pok; jar FULL = pop; pour = pok. peak_db -4.
- Shipped sample: seed 1, 34.87 s, -13.9 LUFS, flash_check PASS. Theme lemon.
- Args: --seed, --spawn, --label, --cap "line1|~line2~", --melody.
- Owner review 2026-10-03: FAVOURITE of the 10 samples.

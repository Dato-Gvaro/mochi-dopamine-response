# bolt_stack

- Rule: Stack game. Block slides in from alternating sides, drops; overhang sliced off and tumbles; perfect = white ring + "Perfect!" + octave chime; 2 perfects in a row regrow the block +22 px.
- Escalation: slider speed 430 -> 2330 px/s ((t/33)^1.6); per-5.8s places [5, 7, 10, 12, 17, 18]. Drops are seeded "player" errors (50% perfect, 12-30 px misses; 75% perfect once width < 170).
- Bolt hops over every incoming block (airborne from slider contact to drop+0.06 s), wobbles harder and sweats as the top narrows.
- Camera follows top at CAM_KEEP=380; a cloud haze hides the tower below ~0.70h so the counter band stays clean.
- Sound: blue_danube note + pok per place, snap on slice, bounce on Bolt landing, hiss on reset.
- Loop: tower sinks into the base block while camera returns; slider ghost fades in at its frame-0 spot.
- s1: 34.6 s, 69 levels, -14.0 LUFS, flash_check 5 flashes / worst 2 per s (reset sky sweep) = PASS.
- Owner review 2026-10-03: Interesting; wants a version with both characters competing side by side.

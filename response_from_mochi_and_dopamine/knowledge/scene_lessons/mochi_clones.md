# mochi_clones

- Rule: plinko; a mini Mochi landing in an x2/x3 slot comes back as 2-3 new minis dropped from the top. Cap 200 (counter = total made).
- physics2d: g=1400, mini e=0.32 (higher e pushed the first landing past 5 s), MR=23, pegs r=11 on a 100 px grid, 10 rows.
- Escalation is pure exponential; pegs/5.7s [23, 77, 266, 845, 1556]; ~100 live at the end. TAIL_S=1.7 after the 200th.
- Sound: peg ping = kit.penta_note by row (high at top), thinned to 0.05 s; landing = twinkle note +12 + small pop, thinned 0.06 s.
- Loop: crowd pops away staggered, one Mochi fades in at the spawn spot.
- s1: 30.2 s, -14.0 LUFS, flash_check 2 flashes = PASS.
- Owner review 2026-10-03: Interesting; wants both characters together, competing.

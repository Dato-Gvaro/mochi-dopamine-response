# mochi_dodge
- Rule: every WALL bounce spawns a new ball at the bounce point, launched toward the arena centre (+-0.5 rad). Balls ignore each other.
- Mochi AI: steer away from predicted closest approaches + near repulsion + centre pull; a touching ball boinks off (Bonks counter).
- Children aimed at the centre is load-bearing: free-angle children graze the wall and cascade, putting 95% of spawns in the last 5 s.
- Starts with 2 balls; ends the instant ball 200 spawns. seed 6, speed 175 px/s: 29.6 s, spawns/5s 6, 8, 19, 42, 123; bonks 3, 1, 5, 7, 21.
- Loop: balls fade/pop out, Mochi glides to centre, the 2 frame-0 balls grow back (RESET 1.6 s).
- Sound: spawn = turkish_march note + pok (thinned 0.06 s); bonk = bounce + squash. peak_db -4.
- Shipped sample: 31.23 s, -13.9 LUFS, flash_check PASS. Theme mint.
- Args: --seed, --speed, --label, --cap, --melody, --dry (sim stats only).
- Owner review 2026-10-03: Too slow at the start; the first 2 s made them want to swipe.

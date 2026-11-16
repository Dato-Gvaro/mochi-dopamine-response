# mochi_tries — tries until success

- Rule: Mochi springs at a cup on a block tower; each miss (floor splat, tower-face splat, backboard splat, rim bonk) resets, and the next try fires SOONER (interval 2.7 s -> 0.40 s, flight sped up to 2.1x), so up to 3 Mochis are in the air at once. The aim converges (error ~ (1-k/n)^1.5, alternating sign), so late misses are rim bonks.
- Flights are analytic ballistic arcs fitted to the contact point through a shared apex, so no physics engine is needed. A time warp (tau) gives the final try slow motion.
- s1: 32 tries, 33.0 s, korobeiniki on launches, squash/pok on impacts, sparkle pops in the celebration. Theme sky.
- Density per 5 s: [6, 9, 18, 28, 31, 31]. The last bin holds slow-mo + celebration + reset; the celebration pops keep it level, not falling.
- Loop: Mochi hops out of the cup back onto the launcher (frame-0 pose). Caption and counter are at alpha 0 at both seam frames.
- Measured: -13.9 LUFS, -3.3 dBTP, flash_check 0.
- Owner review 2026-10-03: OK, not a favourite.

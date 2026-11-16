# mochi_feast4 — Bolt stomps the candy bag, Mochi fills the tank

- Built from the owner's feast3 notes. (1) Two shelves sloping in at Mochi fill the empty middle. (2) Candy doesn't fall by itself: Bolt stomps a candy bag with an EVIL GRIN (mood "angry" + mouth "grin", eyes on Mochi) and every stomp squirts a burst out of the spout. (3) Mochi gets big fast.
- Stage = feast3's tank with the top at y 600. Shelves are on the back wall (hinge at the wall, y 860, 300 px, 25 deg). Mochi grows IN FRONT of them, so they disappear behind it as it grows (a built-in progress bar). Plank + bag + Bolt sit on the top-left corner. Mochi is clipped by the glass AND the plank's underside, so at FULL it is pressed flat into that corner.
- Burst: candies alternate between the left shelf (short toss), the right shelf (long toss across the tank) and straight at Mochi. Late on, the long tosses are eaten in flight by the giant Mochi.
- Escalation: stomp interval 0.85 -> 0.32 s, burst 3 -> 5 candies (ramp over TF 19 s). Bites per 5 s [20, 32, 47, 73].
- Growth: x1 -> x7 over 172 bites, r ~ bites^0.5 (front-loaded). x2 at 1.0 s, x3 5.0, x4 9.0, x5 13.2, x6 17.0, FULL x7 20.3 s.
- Ending: FULL! -> the tank jolts -> Bolt is thrown up (shock), lands squashed, glares at the camera (annoyed), then the evil grin returns before the seam. BURP back to x1.0; 5 ballistic burp candies land exactly on frame 0.
- s1: 22.40 s. check_loop SEAM EXACT. check_clip: -14.00 LUFS, peak -5.0 dBFS, last 0.5 s -42.5 dBFS, seam mean delta 0.281. flash_check 0.
- Bite times barely depend on the seed (the stomp schedule sets them); the seed only changes colours and paths.
- Owner review 2026-10-04 (batch 5): Bolt's stomp station gets covered by big Mochi; make the tank smaller so FULL comes sooner -> mochi_feast5.

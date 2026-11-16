# mochi_feast5 — smaller tank, Bolt's stomp station outside it

- Built from the owner's feast4 note: "the thing that drops balls gets over the main character when he is too big; make the tank little so he can get full size sooner".
- Tank inner 234..846 (612 px, 0.57 W), top y 590, floor 1345. FULL = x5.0 (R0 60 -> R_END 300, wall to wall). Mochi incl. its tuft (top ~637) stays inside the tank; it is clipped only by the side glass.
- Bolt's station is OUTSIDE the tank: a plank bolted to the left wall's top plus a post to the table. Bag on the plank, spout over the rim at (264, 612). Giant Mochi never reaches it.
- Burst candies leave the spout one every 3 frames. Spawning a burst on top of itself made the overlap solver fling candies over the wall (seen in a still: a candy on the table).
- Shelves 180 px at y 900, 25 deg. Stomps 0.85 -> 0.32 s, burst 3 -> 5 (ramp over TF 15 s). Growth r ~ bites^0.5 over 134 bites: x2 2.2 s, x3 7.4, x4 12.4, FULL x5 16.3 s.
- s1: 18.40 s. Bites per 5 s [23, 37, 74].
- Silent tail: the burp is moved to d 0.50, no spray poks, burp pop 0.4 / gain 0.7. The last sound is 1.58 s before the end; last 0.5 s peak -61.7 dBFS (the owner's limit is -60). Marimba + reverb decays ~50 dB/s, so a sound needs ~1.1 s to reach -60.
- check_loop SEAM EXACT. check_clip: -14.01 LUFS, peak -7.5 dBFS, seam mean delta 0.303. flash_check 0.
- Owner review 2026-10-04: Too similar to bolt_feast; owner prefers bolt_feast (moved to Oct 7). Pulled.

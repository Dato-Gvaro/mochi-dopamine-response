# mochi_feast3 — candy feast in a glass tank ("Will it fit?")

- Built from the owner's feast2 review: "something is missing, maybe side walls". The scene now has a STAGE. A glass tank fills 0.88 W (outer x 66..1014, top y 520, floor 1345) and sits on a wooden table. A candy dispenser jar sits over the tank, and Bolt sits on a plank across the tank's top-left corner.
- Rule: every candy makes Mochi BIGGER. The dispenser speeds up (2.2 + 0.06 t^1.5 per s). Mochi grows from x1.0 to x7.0 over 130 bites (r ~ bites^0.65). At x7.0 its widest point touches both glass walls (R_END = 456/1.02).
- FULL!: on the last bite Mochi presses flat against the glass (body clipped to the tank's inside, boing sx 1.12). A "FULL!" sticker shows, the tank jolts (9 px, decays in 0.5 s) and Bolt bounces 120 px, lands (wince) and glares at the camera (annoyed). Then the BURP takes it back to x1.0.
- Bolt reacts: wow at x2 and x4, worried from x6 until FULL.
- Eat test uses Mochi's real outline (half-width table of toon._body_path), not a circle, so nothing survives in the corners. Floor candies are pulled toward Mochi (SUCK_ACC 900). Candy mu must be ~0: mu 0.05 applied every substep of resting contact caps the floor roll at ~80 px/s.
- Bite times are set by the spawns: candies from the nozzle land on Mochi, so every seed gives the same bites per 5 s. The seed only changes colours and bounce paths.
- Loop: the burp spits 5 ballistic candies that land EXACTLY in frame 0's state. check_loop: SEAM EXACT.
- s1: 26.50 s (24.4 s feast + 2.1 s reset). Bites per 5 s [19, 24, 35, 52]. Milestones x2 2.4 s, x3 7.4, x4 12.6, x5 17.0, x6 21.0, x7 24.4.
- Caption is shrunk to y_f 0.098 / size 70 so line 2 clears the dispenser lid.
- Measured (Full HD, check_clip): -14.01 LUFS, peak -7.6 dBFS, last 0.5 s -45 dBFS, seam mean delta 0.276, flash_check 0. check_clip's events/5 s [16, 23, 29, 42, 41]: the last bin holds the 2.1 s reset, which has no bites.
- Owner review 2026-10-03 (batch 4/5): Middle too empty: add / \ shelves; Bolt should cause the drops by jumping (evil smile); grow faster -> mochi_feast4.

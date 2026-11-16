# mochi_feast2 — candy feast, fast start + Bolt watching

- Redesign of mochi_feast (owner: "growth is very slow"). Same rule: every candy Mochi eats makes it BIGGER; the rain gets heavier.
- Fast start: frame 0 already has the burp's candies falling onto Mochi (first bite 0.03 s, 7 bites in the first 0.8 s); rain is shot down at 500 px/s so it arrives in ~0.7 s.
- Growth: r = 64 -> 384 (x1.0 -> x6.0) over 130 bites, r ~ bites^0.65 (first bite +19%), squash-pop every bite. "Size x1.0" counter pops yellow at each whole number. x2 at 3.5 s, x3 9.3, x4 16.1, x5 22.0, x6 26.9.
- Root-cause fix vs mochi_feast: Mochi is NOT a physics body. A static ball bounced fast candies away inside a substep, so they escaped the eat test (the original's slowness). Candies on the shallow bowl get an extra roll toward Mochi (ROLL_ACC).
- Bolt (r 62, left ledge x 92, drawn in front of Mochi): wow at x2 and x4, worried (sweat) from x5 to the end, final chomp BOING (sx 1.17) shoves it to the screen edge -> wince -> annoyed at the camera -> hops home. Idle = blink + look at Mochi's face.
- Loop: Mochi BURPS back to x1.0 ("BURP!" sticker); the 7 spat candies are ballistic and land EXACTLY on frame 0's candy state. check_loop: SEAM EXACT (0/255).
- s3: 28.72 s (26.9 s feast + 1.8 s reset). Bites per 5 s [15, 20, 25, 28, 42]. Seeds 1-12 tried, s3/s7/s12 climb monotonically.
- Sound: entertainer note + soft squash per bite, octave sparkle on milestones, poks for Bolt, boing + pop for the burp. Tail silent (last 0.6 s peak -39 dB).
- Measured (Full HD): -14.0 LUFS, -6.3 dBTP, flash_check 0, post-encode seam mean delta 0.33.
- tools/check_clip.py crashed in its ffmpeg frame grab on this PC (exit 2880417800, `-vsync 0`); measured with ffmpeg ebur128 + numpy instead.
- Owner review 2026-10-03 (batch 2): Something is missing - maybe side walls or similar; rework later.

# slinky_race — "Can Bolt pull a slinky down faster than gravity?" (batch72, NEW)

- Brief: docs/BRIEF_batch72.md §1. New file `scenes/slinky_race.py`.
- Model (SI): N 60 coils, M 0.215 kg (classic metal slinky), closed 0.065 m, hanging 1.25 m; per-gap stiffness k_s 52.5 N/m (pull-only above the closed gap g0), a no-pass contact (stacked clusters move as one, momentum kept; Bolt's hand is kinematic), hanging in true equilibrium (gap i carries the weight below). dt 1e-5 s, no randomness. Pop = the bottom coil moves 12 mm (the balloon's top).
- Results: free drop (Mochi): bottom starts to move at 285.9 ms, pop 290.1 ms → T = 290 ms, L/T = 4.31 m/s. Yanks: 0.5 m/s pop 494 ms, 1 → 462, 2 → 409, 4 → 299 (Mochi by 9 ms), 8 → 150 ms (BOLT). In every case the bottom stays still until the stack arrives.
- Clip: ×8 slow, 5 rounds (round 1 starts mid-fall at 60 ms), hold 0.45 s, re-hang 0.25 s, finale 1.5 s; 17.15 s.
- Music: Mozart, Ein musikalischer Spass K. 522, I (Mutopia, PD): violin I top line, one pizz/harp note per 4 coils added to a stack (≥85 ms apart per side); balloon pops (audio.synth_balloon_pop); F-major chord on Bolt's winning pop.
- Checks (encoded Full HD, label b72): 1029 f = 17.15 s; −14.01 LUFS, peak −4.4; flash PASS; seam 0.67. Frames read 0.1, 2.2, 12.75, 14.9, 15.3, 16.0 (+ Fast stills).
- Doubts: seconds 5-10 are quieter (−22.5 dB RMS: the slow yanks have few stack clacks); the slinkies are small at phone size; the yank is an instant velocity step (an ideal hand).
- Delivered review/batch72/slinky_race.mp4. Owner review: pending.

# mochi_dodge3
- Copy of mochi_dodge2 per owner review ("starts when there is already action; start with ONE or TWO balls and make them FASTER"). mochi_dodge2.py untouched.
- Frame 0: 2 balls at 300 px/s (1.7x the original 175). Ball 0 hits the upper-right wall at ~0.17 s; ball 1 chases Mochi from the right, misses at ~0.17 s (close call on screen at frame 0), then hits the near left wall (spawn #2 at ~1.3 s). Mochi starts mid-dodge at P0 = (CX-170, CY+30). Mochi vmax 600 (accel 6x vmax/s).
- Cap 300 (BR 17): 2 fast balls reach 200 in ~16-18 s; 300 adds ~1.5 s. Coverage at 300 is similar to dodge2 at 200 (BR 20). Speed 330 shortened the clip to ~19 s; 300 is the compromise.
- End: Mochi scoots back to P0 in 0.7 s (MOVE), so the laugh and the payoff play mid-left, away from the Shorts button column. Bolt payoff, pop, grow-in loop, and sound are unchanged from dodge2.
- `--search` also needs the second spawn at <= 1.8 s.
- s18: 22.83 s, t_end 19.93; counter 2 / 3 / 4 at 0 / 0.5 / 1.5 s, 32 at 10 s, 263 at 19 s; 69 close calls, 45 bonks; Bolt cheers at 0.25 s and 10.95 s.
- Shipped sample (batch6): -14.0 LUFS, peak -6.6 dBFS, last 0.5 s -81 dBFS, flash_check PASS (2 in worst 1 s at 19.7 s), seam post-encode mean 0.28-0.31.
- Args: --seed, --speed, --n0, --nmax, --vmax, --label, --cap, --melody, --search, --dry.
- Owner review 2026-10-05: Good, but the first balls should be shot from a ball gun by the other character -> dodge_gun.

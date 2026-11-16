# mochi_bolt_race — Mochi vs Bolt down the marble run

- Two MIRRORED lanes share one ramp schedule (slope 0.20 -> 0.44, a peg-field drop every 3rd ramp), with bumps and pegs seeded per lane, so the lead swaps. Same-lane racing gave almost no overtakes, because circles on one ramp can't pass each other.
- physics2d friction is applied on EVERY contact substep, so the racers use mu=0. Bumps sit only in the lower half of a ramp with about 5 px of protrusion, pegs stay 2R+22 from the walls, and a racer with no progress for 0.8 s does a deterministic hop. Without these, about 80% of seeds jammed.
- Review fix 1: an opaque theme-coloured header (0 to 0.17h, with a 46 px soft fade) is drawn OVER the track, because the scrolling ramps were crossing the caption.
- Review fix 2: racers are 1.4x bigger (RB 38 -> 53) and the drop gap went 128 -> 178. This re-rolled the races and s21 no longer qualified.
- `--search N` lists finish time, gap and lead changes. Current pick s54: Bolt wins by 0.42 s, 7 lead changes, 0 stall-hops, finish 24.6 s, clip 28.8 s. Hits per 5 s [32, 32, 36, 33, 40]. Alternative: s39 has 9 lead changes and a 0.55 s gap.
- la_cucaracha plays on bump and peg hits, with pok on ramp landings, bounce on walls and pops for the finish cheer. Theme lemon. A MOCHI vs BOLT progress bar sits in a solid band at 0.67-0.71h.
- Loop: cross-fade from the finish bowl to frame 0 (the start gate).
- Measured (s54): -14.0 LUFS, -1.1 dBTP, flash_check 0.
- Owner review 2026-10-03: Interesting but can get better.

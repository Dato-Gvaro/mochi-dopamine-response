# longform_shapes: "One ball, crushed until it is more pieces than ATOMS IN THE UNIVERSE"

- Brief: docs/BRIEF_longform2.md (owner 2026-11-09: "press split long video like the sun one, with different tools and new shapes ... different methods for each one, something in the theme of the shape; no meteor").
- Fork of `scenes/longform_atom.py` (`--crushers` path, the "Crushing the Sun" video). longform_atom.py is untouched (bit-reproducible). Same physics (press_split2 PBD), same opening (jars 1-2 whole, pours, jar 3 = the ever-deeper zoom "column"), same drop transitions, HUD layout and Mochi & Bolt reactions.
- Nameable change vs the Sun video: SHAPES. Each chapter has its own shape, its own shape-themed crusher and its own split rule; the video is one chain (each chapter's first crush turns the last chapter's shape into its own).
- Status (2026-11-10): STOPPED before any render: the owner switched the long video to VEHICLES. What exists and what is reusable: `<VIDEOS_DIR>\MochiAndBolt\review\longform2\PROGRESS.md`.
eview\longform2\PROGRESS.md`.
eviewongform2PROGRESS.md.

## The stake (end state at frame 0)
- Goal meter from frame 0: "GOAL: MORE PIECES THAN ATOMS IN THE UNIVERSE (~10^80)", a log bar 10^0 -> 10^80 with the milestones on it.
- The counter is EXACT (a Python big int: the product of every split factor); the last wave crosses 10^80 on the music's last chord.
- Milestone banners ("MORE THAN ...!", estimates marked ~): people on Earth 8.1x10^9, sand grains on all beaches ~7.5x10^18, Rubik's Cube positions 4.3x10^19, stars in the observable universe ~3x10^23, atoms in a human body ~7x10^27, bacteria on Earth ~5x10^30, IPv6 addresses 3.4x10^38, water molecules in the oceans ~4.5x10^46, atoms in the Earth ~1.3x10^50, atoms in the Sun ~1.2x10^57, ways to shuffle a deck (52!) 8.1x10^67, atoms in the observable universe ~10^80.

## Chapter plan (v1, 2026-11-09)
Rules are honest: balls keep VOLUME (the press-split identity, x3^(-1/3)); flat shapes keep AREA. "exact" = a true dissection (the pieces tile the parent).

| Ch | Shape | Crusher (physics family) | Split rule | Splits (n) | Pieces after | Approx. time |
|---|---|---|---|---|---|---|
| 1 | BALLS | BOWLING BALL (top tool, round face; as wide as the jar) | 1 ball -> 3 balls, same total volume (x0.693 size) | 13 (0-13) | 3^13 = 1,594,323 | 0:00-1:00 (jar 1, pour, jar 2, pour, jar 3 column) |
| 2 | SQUARES | GRID CUTTER (top: a steel frame of taut wires, a fry-cutter grid) | first: ball -> 4 squares (same area); then square -> 4 squares (2x2 cut, exact) | 20 (13-33) | x4^20 ~ 1.8x10^18 | 1:00-2:25 |
| 3 | STARS | FIREWORK SHELL (radial: lands, dives in, the fuse burns, it bursts) | every piece -> 5 stars, same total area ("fireworks make stars") | 20 (33-53) | x5^20 ~ 1.7x10^32 | 2:25-3:45 |
| 4 | HEXAGONS | HONEYCOMB PRESS (top: a press plate with a hex-cell face) | every piece -> 7 hexagons (a honeycomb flower), same total area | 21 (53-74) | x7^21 ~ 9.4x10^49 | 3:45-5:05 |
| 5 | TRIANGLES | PRISM + LIGHT BEAM (radial: a white beam through a glass prism, a rainbow ring) | first: hexagon -> 6 triangles (exact); then triangle -> 4 (midpoint cut, exact) | 20 (74-94) | x6 x 4^19 ~ 1.5x10^62 | 5:05-6:25 |
| 6 | DIAMONDS (finale) | JEWELLER'S CLEAVER (swing: a blade on a pivot) | first: triangle -> 4 diamonds (same area); then diamond -> 9 (3x3 cut, exact) | ~19 (94-113), as many as the 10^80 crossing needs | > 10^80 | 6:25-~9:00, last wave on the last chord |

- Total: ~113 splits, **~9:00** (the planner prints the exact table: `python scenes/longform_shapes.py --plan`).
- Chapter transitions = the Sun video's drop (the crusher's last hold, the front glass cracks, the floor gives, the column falls into the next machine), banner "NEXT SHAPE: STARS". Jar 3's end is a true "JAR FULL" (balls grow the pile x1.44 per split); the flat-shape chapters do not grow the pile (area kept), so their end banner never says FULL.
- Music: Brahms, Hungarian Dance No. 5 (pub. 1869, Brahms d. 1897: PD), melody from the flutetunes MIDI (as sand_rise4 / growth_race) + our own oom-pah harmony, on our accelerating tempo map; the theme's 4 statements looped with fuller orchestration per block, the F#-minor cadence = the 10^80 payoff. Not Grieg, not kid-coded.
- Palette: one hue family per shape on a dark lab background: balls orange/red, squares cyan, stars gold, hexagons lime, triangles magenta, diamonds violet-ice.

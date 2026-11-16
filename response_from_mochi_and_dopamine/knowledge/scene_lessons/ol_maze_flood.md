# ol_maze_flood (DopamineEXE, batch75 #2): stills stage
- A top-down 7x7 maze (growing-tree seed 74: 10 dead ends, route 26 cells, the exit is the farthest cell). The valve pipe enters top-left; the exit cup sits under the bottom-middle cell. Caption `Water fills ^EVERY^ path…|until it finds the ~EXIT~`.
- Physics: PBD discs (no gravity), weak cohesion 0.06, XSPH 0.03, and a GLOBAL DENSITY PROJECTION each frame (Poisson on a 26 px MAC grid aligned with the walls). Without it the PBD compressed 2.3x near the source (11.6k balls in a 6.1k-capacity maze). With it: 6,156 balls.
- Defaults Q0 47/s, x2 every 2.5 s from 0.5 s (x16 = 752/s), pre-roll 10.5 s. Exit 12.65 s, cup full 13.12 s, clip 15.12 s. Cells flooded/s: 1,0,2,2,1,1,5,3,8,6,6,7,5, then the cup gush.
- HUD: meter = PATHS FLOODED n/49 + cup -> SOLVED!; counter = balls with a VALVE xN pill. Finale = the one route drawn in gold.
- Not built yet: the clip render and the sound pass.
- Full HD (batch75 round 2): pre-roll 15.7 s at Q0 42 (frame 0 = first corridor full, 4/49). The dissolve hard-swaps the HUD (no doubled numbers). Music: Bach Passacaglia BWV 582 (Mutopia PD, first use): one variation at quarter = 96, cup-full on the beat-118 cadence + a C-major chord. A chime per flooded cell. 15.73 s, -14.0 LUFS, flash PASS. Delivered `<VIDEOS_DIR>\DopamineExe\review\batch75\ol_maze_flood.mp4`.

## v2 (`scenes/ol_maze_flood2.py`, overnight 2026-11-12, brief docs/BRIEF_overnight_1112.md §4; v1 untouched)
- Owner: v1 "kinda sticky, unpleasant to see". Keep the idea; the particles must read as real LIQUID.
- Model: no particles.
  - A 2 px grid of the open floor and a 16-neighbour Dijkstra from the pipe. Knight and diagonal moves need the passed cells open, or the front jumps the 5 px walls.
  - Speed dips 22% at a wall (low wall friction, a gentle Poiseuille bulge).
  - Incompressible: cells flood in path order at exactly the valve's area rate, so a split slows each branch and a dead end speeds up the others.
- Render:
  - wet mask (+ wall band next to the water) + splash droplets → Gaussian σ 2 cells → smoothstep threshold = one merged sheet;
  - height = blur of the sheet → normals → diffuse + specular (power 40) + a darker meniscus rim;
  - dye = the rainbow by arrival time; the pipe carries the current dye.
- Splashes: the front hitting a wall head-on (flow · wall normal < −0.55) throws reflected droplets (90-230 px/s, 0.18-0.34 s) that merge back into the sheet.
- Valve x2 at 0.3, 1.4, 2.9, 5.0 s (x16), A0 12% (frame 0). Exit 10.1 s, cup full 10.6 s, clip 12.6 s.
- FAST check (the old ladder): −14.00 LUFS, flash 1/s. The x16-at-6.4 s ladder looked slow for 3 s; it was compressed.

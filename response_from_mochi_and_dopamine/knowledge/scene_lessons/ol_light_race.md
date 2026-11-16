# ol_light_race (DopamineEXE, BRIEF_dopa_1113 clip 5)
- Six racers from Earth to the Moon (384,400 km) at true paces. A monotone time warp lets each finish in turn: light 1.28 s, Apollo 11 3 d 4 h, jet 17.8 d, car 160 d, walking 8.8 y, snail 12,181 y.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_light_race\` (FHD, 14.23 s). README there holds the rung table and sources.

## How it works
- **Music clock:** Mountain King (Mutopia 1888), beats 20→68. Tempo is exponential per beat, 2.4→7 b/s (`t_of_b`). Arrivals sit on beats 22/28/30/40/52/68.
- **Warp:**
  - log10(rate) is piecewise linear between arrivals and never falls.
  - Each knot is solved by bisection, so the race clock hits each racer's true time exactly at its arrival frame.
  - Before light lands, time is real (×1).
- **Feasibility:** rocket→jet is only 5.6x in race time, so equally spaced arrivals would force the warp to SLOW down. The beats were searched (scratch `warp.py`) for a set where the rate only rises. The rocket and jet then land 0.7 s apart.
- **Clock display:** the clock is quantised to melody-note onsets (a visible tick per note). The racers move continuously.
- **Art reuse (read-only):** Saturn V, the car and the person come from ol_domino_style_test2; the jet, Earth and Moon from ol_domino3_objects. The snail is drawn in cairo here.

## Checks
- FHD fhd2: -14.0 LUFS, TP -5.0, flash PASS (0), seam 0.46 (steps 0.2-0.6).
- Gotcha: the Saturn V art's nose points +x from its origin. Draw it a body length back, or it hides under the Moon at the finish.
